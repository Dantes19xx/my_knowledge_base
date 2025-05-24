# Dunder Method: __iadd__

## Назначение

Метод `__iadd__` используется для реализации **операции присваивания со сложением** (`+=`).  
Позволяет модифицировать объект на месте (если это имеет смысл), либо вернуть новый объект, как в обычном `__add__`.

---

## Сигнатура

```python
def __iadd__(self, other):
```


- `self` — объект слева от `+=`
    
- `other` — объект справа
    
- Возвращает **объект, который будет заменён в переменной** (обычно `self` или новый объект)


---


## Когда вызывается

|Выражение|Что вызывается|
|---|---|
|`a += b`|`a.__iadd__(b)`|
|Если не реализован, Python вызывает `a = a + b` → `__add__`|

---
## Пример: in-place сложение

```python
class Counter:
    def __init__(self, value):
        self.value = value

    def __iadd__(self, other):
        self.value += other
        return self

    def __repr__(self):
        return f"Counter({self.value})"

c = Counter(10)
c += 5
print(c)  # Counter(15)
```

> Объект `c` модифицируется **на месте**, и сохраняет свою идентичность: `id(c)` не меняется.


---

## Поведение по умолчанию

Если `__iadd__` не определён, Python пытается выполнить

```python
a = a + b  # т.е. вызывает __add__ и присваивает результат
```

В этом случае `id(a)` после `+=` может измениться.


---
## Пример: сравнение **add** и **iadd**

```python
class Vector:
    def __init__(self, values):
        self.values = values

    def __add__(self, other):
        return Vector(self.values + other.values)

    def __iadd__(self, other):
        self.values += other.values
        return self

    def __repr__(self):
        return f"Vector({self.values})"

v1 = Vector([1, 2])
v2 = Vector([3, 4])
v3 = v1 + v2       # создаёт новый объект
v1 += v2           # изменяет v1 на месте
print(v1)          # Vector([1, 2, 3, 4])
print(v3)          # Vector([1, 2, 3, 4])
```


---

## Рекомендации

- Возвращайте `self`, если вы **изменяете объект на месте**.
    
- Возвращайте **новый объект**, если хотите, чтобы `+=` работал как `+`.
    
- Следите за тем, чтобы `__iadd__` не нарушал принцип неожиданности (surprise principle): `+=` должен вести себя предсказуемо.
    

---

## Связанные методы

- [[__add__]] — обычное сложение
    
- [[__radd__]] — обратное сложение

#dunder #python 

