## Описание

**Dict comprehension** — это компактный способ создания словарей на основе итерируемых объектов.  
Аналогичен [[List Comprehension]], но создаёт словарь `{ключ: значение}`.

Синтаксис:

```python
{key_expr: value_expr for item in iterable if condition
```

---

## ✅ Примеры

### 1. Квадраты чисел

```python
squares = {x: x * x for x in range(5)} # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16
```

### 2. Фильтрация по условию

```python
even_squares = {x: x * x for x in range(10) if x % 2 == 0} # {0: 0, 2: 4, 4: 16, 6: 36, 8: 64}
```

### 3. Инвертирование словаря

```python
original = {'a': 1, 'b': 2, 'c': 3} inverted = {v: k for k, v in original.items()} # {1: 'a', 2: 'b', 3: 'c'}
```

### 4. Создание словаря из списка кортежей

```python
pairs = [('x', 1), ('y', 2), ('z', 3)] result = {k: v for k, v in pairs} # {'x': 1, 'y': 2, 'z': 3}
```

---

## ⚙️ Эквивалент с `for`-циклом

```python
# dict comprehension
squares = {x: x * x for x in range(5)}

# обычный способ
squares = {}
for x in range(5):
    squares[x] = x * x

```

---

## 💡 Когда использовать

- Быстрое создание словарей из списков, множеств или других словарей.
    
- Преобразование данных в удобный формат.
    
- Чистый и читаемый код при простой логике.
    

---

## 🛑 Когда НЕ использовать

- Слишком сложные условия → ухудшается читаемость.
    
- Повторяющиеся ключи → может возникнуть нежелательное поведение (последнее значение затирает предыдущие).
    

---

## 🧠 Связанные темы

- [[List Comprehension]] → `[x for x in iterable]`
    
- [[Set Comprehension]] → `{x for x in iterable}`
    
- `generator expression` → `(x for x in iterable)`