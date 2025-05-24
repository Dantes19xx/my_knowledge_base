# Dunder Method: __str__

## Назначение

Метод `__str__` отвечает за **человеко-читаемое строковое представление** объекта.  
Используется функцией `str()` и при выводе через `print()`.

---

## Сигнатура
```python
def __str__(self) -> str:
```

*Должен вернуть **строку**, описывающую объект понятным образом.*



---

## Когда вызывается

|Ситуация|Поведение|
|---|---|
|`str(obj)`|Вызывает `obj.__str__()`|
|`print(obj)`|Тоже вызывает `obj.__str__()`|
|В f-строке: `f"{obj}"`|Вызывает `__str__()`|

Если `__str__` не определён, вызывается [[__repr__]].


---
## Пример:

```python
class Book:
    def __init__(self, title, author):
        self.title = title
        self.author = author

    def __str__(self):
        return f'"{self.title}" by {self.author}'

b = Book("1984", "George Orwell")
print(b)              # "1984" by George Orwell
print(str(b))         # "1984" by George Orwell
```


---
## Сравнение с `__repr__`

|Метод|Назначение|Используется в|
|---|---|---|
|`__str__`|Для пользователя (`print`)|`str(obj)`, `print(obj)`|
|`__repr__`|Для разработчика, отладки|`repr(obj)`, консоль Python, логи|

---

## Рекомендации

- Используйте `__str__`, чтобы сделать объект более понятным при выводе.
    
- Желательно не делать `__str__` слишком «техническим» — он должен быть **понятным и коротким**.
    

---

## Пример: человекочитаемый вывод

```python
class Temperature:
    def __init__(self, celsius):
        self.celsius = celsius

    def __str__(self):
        return f"{self.celsius}°C"

t = Temperature(22.5)
print(t)           # 22.5°C
```


---
## Что если `__str__` не задан?

Если метод `__str__()` отсутствует, Python по умолчанию вызывает `__repr__()`:


```python
class Empty:
    pass

e = Empty()
print(e)  # <__main__.Empty object at 0x...>
```

#dunder #python 