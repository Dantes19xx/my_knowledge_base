# Dunder Method: __radd__

## Назначение

Метод `__radd__` используется для **обратного сложения**: он вызывается, если левый операнд **не поддерживает** операцию `+` с правым.  
Полезен при смешанных типах (`int + MyClass`), или если `__add__` возвращает `NotImplemented`.

---

## Сигнатура

```python
def __radd__(self, other):
```

- `self` — правый операнд (`b`)
    
- `other` — левый операнд (`a`)
    
- Должен вернуть результат сложения `a + b`


---
## Когда вызывается

|Сценарий|Что происходит|
|---|---|
|`a + b`|Если `a.__add__(b)` вернул `NotImplemented`, Python вызывает `b.__radd__(a)`|

---

## Пример: поддержка `int + MyNumber`

```python
class MyNumber:
    def __init__(self, value):
        self.value = value

    def __radd__(self, other):
        return MyNumber(other + self.value)

    def __str__(self):
        return str(self.value)

a = MyNumber(10)
print(5 + a)  # 15
```

Здесь `5 + a` вызывает `a.__radd__(5)`, потому что `int.__add__(MyNumber)` не знает, что делать.


---
## Сравнение с **add**

```python
class MyNumber:
    def __init__(self, value):
        self.value = value

    def __add__(self, other):
        if isinstance(other, MyNumber):
            return MyNumber(self.value + other.value)
        return NotImplemented

    def __radd__(self, other):
        return MyNumber(other + self.value)

    def __str__(self):
        return str(self.value)

a = MyNumber(7)
b = MyNumber(3)
print(a + b)  # 10
print(5 + a)  # 12
```


---
## Рекомендации

- Возвращайте `NotImplemented` в `__add__`, если `other` неподдерживаемого типа — тогда Python сам вызовет `__radd__` у `other`.
    
- В `__radd__` не обязательно проверять тип `other`, если вы точно знаете, откуда он может прийти (например, число или строка).
    

---

## Связанные методы

- [[__add__]] — обычное сложение
    
- [[__iadd__]] — in-place сложение

#dunder #python 