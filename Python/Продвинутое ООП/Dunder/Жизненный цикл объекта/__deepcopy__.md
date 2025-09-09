# Dunder Method: __deepcopy__

## Назначение

Метод `__deepcopy__` используется для **глубокого копирования** объекта. Это означает рекурсивное копирование всех вложенных объектов, чтобы оригинал и копия были полностью независимы.

---

## Сигнатура

```python
def __deepcopy__(self, memo):
```

- `self` — сам объект.
    
- `memo` — словарь для предотвращения бесконечной [[Рекурсия|рекурсии]] (при копировании объектов с взаимными ссылками).


---
## Пример:

```python
import copy

class Person:
    def __init__(self, name, attributes):
        self.name = name
        self.attributes = attributes

    def __deepcopy__(self, memo):
        print("Вызван __deepcopy__")
        # Копируем name как неизменяемую строку, attributes — deepcopy
        new_name = copy.deepcopy(self.name, memo)
        new_attributes = copy.deepcopy(self.attributes, memo)
        return Person(new_name, new_attributes)

p1 = Person("Alice", {"age": 30})
p2 = copy.deepcopy(p1)

print(p1 is p2)                      # False
print(p1.attributes is p2.attributes)  # False (глубокая копия)
```


---

## Поверхностное vs глубокое копирование

| Тип копирования | Описание                                    |
| --------------- | ------------------------------------------- |
| [[__copy__]]    | [[Поверхностное копирование]] (`copy.copy`) |
| `__deepcopy__`  | Глубокое копирование (`copy.deepcopy`)      |

- Поверхностная копия копирует ссылки на вложенные объекты.
    
- Глубокая копия создает **полные рекурсивные копии** всех вложенных объектов.
    

---

## Зачем нужен параметр `memo`

- Используется для **обхода циклических ссылок**.
    
- `memo` — словарь вида `{id(obj): copy_of_obj}`, куда Python сохраняет уже скопированные объекты.
    
- При повторной попытке копировать тот же объект — результат берётся из `memo`.


---

## Пример с циклическими ссылками


```python
import copy

class Node:
    def __init__(self, value):
        self.value = value
        self.next = None

    def __deepcopy__(self, memo):
        if id(self) in memo:
            return memo[id(self)]
        copied = Node(self.value)
        memo[id(self)] = copied
        copied.next = copy.deepcopy(self.next, memo)
        return copied

a = Node(1)
b = Node(2)
a.next = b
b.next = a  # Цикл

copy.deepcopy(a)  # Без зацикливания благодаря memo
```

## Когда использовать

- Когда в объекте есть **вложенные изменяемые структуры**, и важно сделать их независимыми.
    
- Когда `copy.deepcopy()` по умолчанию копирует объект неправильно или вызывает побочные эффекты.

#dunder #python 
