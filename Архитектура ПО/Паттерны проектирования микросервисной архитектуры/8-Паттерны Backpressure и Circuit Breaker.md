✏️ Нагрузка — это интенсивность взаимодействия пользователя с приложением. Чем более активны пользователи и чем их больше, тем выше нагрузка. Приложения с высокой нагрузкой называют **высоконагруженными** (high-load) приложениями.

### Метрики:
- **DAU (Daily Active Users)** — количество пользователей в день. Также часто используют метрику MAU — Monthly Active Users.
- **RPS (Requests Per Second)** — количество запросов, которые сервер приложения обрабатывает в секунду.
- **QPS (Queries Per Second)** — количество запросов в секунду к базе данных.

# Паттерны проектирования: Backpressure и Circuit Breaker

## 📦 Backpressure (Обратное давление)

**Описание**:  
Backpressure — это паттерн управления потоком данных, применяемый в ситуациях, когда производитель генерирует данные быстрее, чем потребитель может их обработать. Это может привести к перегрузке, утечке памяти и сбоям.

**Цель**:  
Предотвратить перегрузку потребителя за счёт управления объемом поступающих данных.

**Применяется в**:
- Очередях сообщений (RabbitMQ, Kafka)
- Реактивном программировании (RxPY, asyncio streams)
- HTTP-стриминге

**Способы реализации**:
- Буферизация с ограничением размера
- Ограничение количества параллельных задач
- Явная сигнализация спроса (`request(n)` в реактивных стримах)
- Отбрасывание или отклонение входящих данных при перегрузке

---

## 🔌 Circuit Breaker (Предохранитель)

**Описание**:  
Circuit Breaker — это паттерн отказоустойчивости, который временно прекращает вызовы к внешнему ресурсу (например, API), если тот начинает часто возвращать ошибки или превышает таймауты. Это помогает избежать каскадных сбоев и снижает нагрузку на систему.

**Цель**:  
Защитить систему от деградации при сбоях во внешних зависимостях.

**Применяется в**:
- Сетевых вызовах (HTTP, RPC)
- Микросервисах
- API Gateway
- Любом внешнем ресурсе, с которым возможны сбои

**Состояния**:
- `Closed`: Все запросы выполняются.
- `Open`: Запросы блокируются и сразу завершаются ошибкой.
- `Half-Open`: Проверочные запросы для определения, восстановился ли сервис.

---
```python
#Backpressure

import queue
import threading
import time

q = queue.Queue(maxsize=5)

def producer():
    for i in range(20):
        try:
            q.put(i, timeout=1)  # блокирует, если очередь полна
            print(f"Produced: {i}")
        except queue.Full:
            print("Queue is full! Dropping data.")

def consumer():
    while True:
        try:
            item = q.get(timeout=2)
            print(f"Consumed: {item}")
            time.sleep(0.5)  # имитация обработки
        except queue.Empty:
            break

t1 = threading.Thread(target=producer)
t2 = threading.Thread(target=consumer)

t1.start()
t2.start()

t1.join()
t2.join()
```

```python
#Circuit Breaker

import time
import random

class CircuitBreaker:
    def __init__(self, max_failures=3, reset_timeout=5):
        self.max_failures = max_failures
        self.reset_timeout = reset_timeout
        self.failure_count = 0
        self.last_failure_time = None
        self.state = 'CLOSED'

    def _should_open(self):
        return self.failure_count >= self.max_failures

    def _should_reset(self):
        if self.last_failure_time is None:
            return False
        return (time.time() - self.last_failure_time) >= self.reset_timeout

    def call(self, func):
        if self.state == 'OPEN':
            if self._should_reset():
                self.state = 'HALF_OPEN'
            else:
                raise Exception("Circuit is open")

        try:
            result = func()
            self.failure_count = 0
            self.state = 'CLOSED'
            return result
        except Exception as e:
            self.failure_count += 1
            self.last_failure_time = time.time()
            if self._should_open():
                self.state = 'OPEN'
            raise e

# Пример использования
breaker = CircuitBreaker()

def unstable_service():
    if random.random() < 0.7:
        raise Exception("Service failed")
    return "Success!"

for _ in range(10):
    try:
        result = breaker.call(unstable_service)
        print("Call result:", result)
    except Exception as e:
        print("Call failed:", e)
    time.sleep(1)
```