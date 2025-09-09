#flask #python #фреймворки #flask_extensions 

**Flask-Redis** — это расширение Flask, которое облегчает интеграцию **[[Redis]]** в приложение.  
Оно предоставляет удобный доступ к Redis-клиенту напрямую через объект приложения Flask.

Redis используется для:

- хранения сессий,
    
- кэша,
    
- очередей задач,
    
- [[Паттерн Pub_Sub|Pub/Sub]] (уведомления и сообщения).
    

---

## Основные возможности

- Простая инициализация клиента Redis в Flask
    
- Поддержка стандартных команд Redis (`set`, `get`, `delete`, `expire` и т.д.)
    
- Хранение любых данных (строки, JSON, бинарные данные)
    
- Используется в связке с **[[Flask-Session]]**, **Celery**, **[[Flask-SocketIO]]**
    

---

## Роль во Flask

Redis — это **in-memory** хранилище (очень быстрое).  
Flask-Redis позволяет легко использовать его в веб-приложениях:

- кэширование данных (например, результатов SQL-запросов),
    
- хранение сессий,
    
- временные токены (одноразовые пароли, подтверждения),
    
- механизмы pub/sub для уведомлений.
    

---

## Типичный рабочий процесс

1. Установка:
```bash
pip install flask-redis
```

2.  Подключение в приложении:

```python
from flask import Flask
from flask_redis import FlaskRedis

app = Flask(__name__)
app.config["REDIS_URL"] = "redis://localhost:6379/0"

redis_client = FlaskRedis(app)
```

3. Использование
```python
@app.route("/set/")
def set_value():
    redis_client.set("username", "dmitriy")
    return "Значение сохранено!"

@app.route("/get/")
def get_value():
    return redis_client.get("username") or "Нет данных"
```


---

## Особенности

- Требует установленный Redis-сервер
    
- Можно подключать несколько баз Redis (по разным `REDIS_URL`)
    
- Очень полезно в микросервисах и масштабируемых приложениях
    

---

📌 **Итог**: Flask-Redis — это расширение, которое интегрирует Redis с приложением Flask и позволяет использовать его для кэширования, сессий, токенов и pub/sub.