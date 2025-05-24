 Dunder Method: __mul__

## Назначение

Метод `__mul__` позволяет переопределить поведение оператора умножения `*` для объектов пользовательских классов.  
Если вы хотите, чтобы `a * b` работало с вашими объектами — реализуйте `__mul__`.

---

## Сигнатура

```python
def __mul__(self, other):
```

- `self` — левый операнд (`a`)
    
- `other` — правый операнд (`b`)
    
- Возвращает результат умножения (обычно новый объект)


---
## Когда вызывается

|Выражение|Что вызывается|
|---|---|
|`a * b`|`a.__mul__(b)`|
|Если не реализован, Python вызывает `b.__rmul__(a)`|


---
## Пример: умножение вектора на скаляр

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __mul__(self, scalar):
        return Vector(self.x * scalar, self.y * scalar)

    def __repr__(self):
        return f"Vector({self.x}, {self.y})"

v = Vector(2, 3)
print(v * 4)  # Vector(8, 12)
```


---
## Обработка несовместимых типов

```python
def __mul__(self, other):
    if isinstance(other, (int, float)):
        return Vector(self.x * other, self.y * other)
    return NotImplemented
```

Возврат `NotImplemented` позволяет Python вызвать `__rmul__` у `other`, если это необходимо.


---
## Рекомендации

- Метод `__mul__` должен быть **чистой функцией** — не изменять исходные объекты.
    
- Возвращайте `NotImplemented`, если тип `other` не поддерживается — это даёт Python возможность вызвать `__rmul__`.
    

---

## Связанные методы

- `__rmul__` — обратное умножение: `b.__rmul__(a)`
    
- `__imul__` — in-place умножение: `a *= b`

#dunder #python 
