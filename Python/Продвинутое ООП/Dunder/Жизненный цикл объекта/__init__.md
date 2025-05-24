# Dunder Method: __init__

## Назначение
Метод `__init__` используется для инициализации нового объекта. Он автоматически вызывается после создания экземпляра класса. Это аналог конструктора в других языках программирования.

---

## Сигнатура

```python
def __init__(self, ...):
```

- `self` — обязательный первый параметр, ссылается на создаваемый объект.
    
- Остальные параметры задаются при создании экземпляра.


---
## Простой пример

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

p = Person("Alice", 30)
print(p.name)  # Alice
print(p.age)   # 30
```

---

## Инициализация значений по умолчанию

```python
class Person:
    def __init__(self, name, age=18):
        self.name = name
        self.age = age

p1 = Person("Bob")
p2 = Person("Eve", 25)
print(p1.age)  # 18
print(p2.age)  # 25
```


---

## Использование с наследованием

```python
class Animal:
    def __init__(self, species):
        self.species = species

class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__("dog")
        self.name = name
        self.breed = breed

d = Dog("Rex", "Labrador")
print(d.species)  # dog
print(d.name)     # Rex
```

`super().__init__()` вызывает `__init__` родительского класса.


---

## Советы по использованию

- Не стоит выполнять тяжелые операции в `__init__`; он должен лишь настроить объект.
    
- Не путай с `__new__`: `__init__` инициализирует уже созданный объект.
    
- Лучше явно указывать все необходимые аргументы — это делает поведение класса предсказуемым.

---

## Когда `__init__` не нужен

Если объект не требует инициализации параметров, можно не определять `__init__`. Python создаст пустой конструктор по умолчанию:

```python
class Empty:
    pass

e = Empty()
```

#dunder #python 
