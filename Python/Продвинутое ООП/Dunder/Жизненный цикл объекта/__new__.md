# Dunder Method: __new__

## Назначение

Метод `__new__` отвечает **за создание нового экземпляра класса**. Это первый метод, который вызывается при создании объекта, ещё до [[__init__]].

Используется в случаях:
- [[Наследование]] от неизменяемых типов (`int`, `str`, `tuple` и др.)
- Реализация паттернов вроде Singleton
- Контроль над созданием экземпляров (например, кэширование)

---

## Сигнатура
```python
def __new__(cls, *args, **kwargs):
```
- `cls` — сам класс, от которого создаётся объект.
    
- Возвращает **экземпляр класса** (обычно `super().__new__(cls)`).


---
## Простой пример

```python
class MyClass:
    def __new__(cls):
        print("Вызван __new__")
        instance = super().__new__(cls)
        return instance

    def __init__(self):
        print("Вызван __init__")

obj = MyClass()
# Вызван __new__
# Вызван __init__
```


---

## Пример с неизменяемым типом (`tuple`)

```python
class Point2D(tuple):
    def __new__(cls, x, y):
        return super().__new__(cls, (x, y))

p = Point2D(1, 2)
print(p)        # (1, 2)
print(p[0])     # 1
```


---

## Использование с `__init__`

```python
class Demo:
    def __new__(cls, value):
        print("Создание объекта")
        instance = super().__new__(cls)
        return instance

    def __init__(self, value):
        print("Инициализация объекта")
        self.value = value

d = Demo(42)
# Создание объекта
# Инициализация объекта
```


---

## Пример: Singleton через **new**

```python
class Singleton:
    _instance = None

    def __new__(cls, *args, **kwargs):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
        return cls._instance

s1 = Singleton()
s2 = Singleton()

print(s1 is s2)  # True
```


---

## Отличия от `__init__`

|`__new__`|`__init__`|
|---|---|
|Создаёт объект|Инициализирует объект|
|Вызывается первым|Вызывается после `__new__`|
|Возвращает объект|Ничего не возвращает (`None`)|
|Используется при наследовании от `tuple`, `str`, `int` и т.п.|Стандартный способ задания параметров|

---

## Когда использовать

- При наследовании от **неизменяемых** типов
    
- Когда нужно **контролировать создание объектов**
    
- Для шаблонов проектирования, таких как **Singleton**, **Flyweight**

#dunder #python 