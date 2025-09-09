# Dunder Method: __sub__

## Назначение

Метод `__sub__` позволяет переопределить поведение оператора вычитания `-` для объектов пользовательских классов.  
Если вы хотите, чтобы `a - b` работало с вашими объектами — реализуйте `__sub__`.

---

## Сигнатура

```python
def __sub__(self, other):
```

- `self` — левый операнд (`a`)
    
- `other` — правый операнд (`b`)
    
- Возвращает результат вычитания (обычно новый объект)


## Когда вызывается

|Выражение|Что вызывается|
|---|---|
|`a - b`|`a.__sub__(b)`|
|Если не реализовано, Python вызывает `b.__rsub__(a)`|

---

## Пример: вычитание точек

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __sub__(self, other):
        return Point(self.x - other.x, self.y - other.y)

    def __repr__(self):
        return f"Point({self.x}, {self.y})"

p1 = Point(10, 5)
p2 = Point(3, 2)
print(p1 - p2)  # Point(7, 3)
```


---

## Обработка несовместимых типов

```python
def __sub__(self, other):
    if isinstance(other, Point):
        return Point(self.x - other.x, self.y - other.y)
    return NotImplemented
```

Это даёт Python возможность вызвать `__rsub__` у `other`, если `other` поддерживает такое поведение.


---

## Пример: разность чисел в оболочке

```python
class WrappedInt:
    def __init__(self, value):
        self.value = value

    def __sub__(self, other):
        return WrappedInt(self.value - other)

    def __repr__(self):
        return f"WrappedInt({self.value})"

a = WrappedInt(10)
print(a - 3)  # WrappedInt(7)
```


---

## Рекомендации

- Операция `a - b` не должна изменять `a` или `b`, она должна быть **чистой** (pure function).
    
- Возвращайте `NotImplemented`, если `other` не подходит — это позволяет Python вызывать `__rsub__` другого объекта.
    

---

## Связанные методы

- [[__rsub__]] — обратное вычитание: `b.__rsub__(a)`
    
- `__isub__` — in-place вычитание: `a -= b`

#dunder #python 
