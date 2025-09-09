## Описание

**Set comprehension** — это лаконичный способ создания множеств (`set`) на основе итерируемых объектов.  
Синтаксис аналогичен `list comprehension`, но создаёт **множество уникальных значений**.

Синтаксис:

```python
{expression for item in iterable if condition}
```

---

## ✅ Примеры

### 1. Квадраты чисел

```python
squares = {x * x for x in range(5)} # {0, 1, 4, 9, 16}
```

### 2. Отбор чётных чисел

```python
evens = {x for x in range(10) if x % 2 == 0} # {0, 2, 4, 6, 8}
```

### 3. Удаление дубликатов из строки

```python
unique_chars = {char for char in "hello world"} # {'r', 'e', ' ', 'o', 'd', 'h', 'l', 'w'}
```

---

## ⚙️ Эквивалент с `for`-циклом

```python
# set comprehension
evens = {x for x in range(10) if x % 2 == 0}

# обычный способ
evens = set()
for x in range(10):
    if x % 2 == 0:
        evens.add(x)
```

---

## 💡 Когда использовать

- Быстрое создание множества уникальных значений.
    
- Удаление дубликатов.
    
- Фильтрация и трансформация итерируемых объектов.
    

---

## 🛑 Когда НЕ использовать

- Когда важен порядок элементов (множество — неупорядоченная структура).
    
- Сложная логика внутри выражения — может ухудшить читаемость.
    

---

## 🧠 Связанные темы

- [[List Comprehension]] → `[x for x in iterable]`
    
- [[Dict Comprehension]] → `{k: v for k, v in iterable}`
    
- `generator expression` → `(x for x in iterable)`