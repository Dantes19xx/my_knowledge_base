# Dunder Method: __add__

## Назначение

Метод `__add__` позволяет переопределить поведение оператора `+` для объектов пользовательских классов.  
Если вы хотите, чтобы выражение `a + b` работало с экземплярами вашего класса — реализуйте `__add__`.

---

## Сигнатура

```python
def __add__(self, other):
```

- `self` — левый операнд (`a`)
    
- `other` — правый операнд (`b`)
    
- Должен возвращать **новый объект** или результат сложения.

## Когда вызывается

|Выражение|Что вызывается|
|---|---|
|`a + b`|`a.__add__(b)`|
|Если `__add__` не определён, вызывается `__radd__` у `b`, если он реализован|

---

## Пример: сложение точек

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Point(self.x + other.x, self.y + other.y)

    def __repr__(self):
        return f"Point({self.x}, {self.y})"

p1 = Point(1, 2)
p2 = Point(3, 4)
print(p1 + p2)  # Point(4, 6)
```


---

## Совместимость с типами

Если `other` — не экземпляр нужного класса, желательно вернуть `NotImplemented`, чтобы дать возможность Python вызвать `__radd__` другого объекта:

```python
def __add__(self, other):
    if isinstance(other, Point):
        return Point(self.x + other.x, self.y + other.y)
    return NotImplemented
```


---
## Пример: сложение со строкой

```python
class Phrase:
    def __init__(self, text):
        self.text = text

    def __add__(self, other):
        if isinstance(other, Phrase):
            return Phrase(self.text + " " + other.text)
        if isinstance(other, str):
            return Phrase(self.text + " " + other)
        return NotImplemented

    def __str__(self):
        return self.text

a = Phrase("Hello")
b = Phrase("world")
print(a + b)         # Hello world
print(a + "!")       # Hello !
```


---

## Рекомендации

- Всегда проверяйте тип `other`.
    
- Возвращайте `NotImplemented`, если операция не поддерживается — это позволяет корректно вызывать `__radd__` у второго операнда.
    
- Никогда не модифицируйте `self` — `__add__` должен быть **чистой** операцией, возвращающей новый объект.
    

---

## Связанные методы

- [[__radd__]] — обратное сложение: `b.__radd__(a)`, если `a.__add__(b)` вернул `NotImplemented`.
    
- [[__iadd__]] — in-place сложение: `a += b`.

#dunder #python 
