#jinja2 #шаблонизатор 

## Базовый синтаксис
Для итерации используется цикл `for`:

```jinja2
{% for item in items %}
  {{ item }}
{% endfor %}
```


---

## Доступ к индексу и служебным переменным

Внутри цикла доступен объект `loop`, у которого есть полезные атрибуты:

- `loop.index` — номер элемента (с 1)
    
- `loop.index0` — номер элемента (с 0)
    
- `loop.revindex` — обратный индекс (с 1)
    
- `loop.revindex0` — обратный индекс (с 0)
    
- `loop.first` — `True`, если первый элемент
    
- `loop.last` — `True`, если последний элемент
    
- `loop.length` — общее количество элементов
    
- `loop.cycle(a, b, ...)` — чередование значений


---

## Условная отрисовка внутри цикла

Можно использовать [[Условия в Jinja2|if]] прямо внутри цикла:

```jinja2
{% for item in items %}
  {% if item.is_active %}
    {{ item.name }}
  {% endif %}
{% endfor %}
```

---

## Пустой список (`else` в цикле)

Если коллекция пуста, можно обработать это:

```jinja2
{% for product in products %}
  {{ product.name }}
{% else %}
  Нет товаров
{% endfor %}
```


---

## Вложенные циклы

Можно использовать вложенные `for`:

```jinja2
{% for category in categories %}
  <h3>{{ category.name }}</h3>
  <ul>
  {% for item in category.items %}
    <li>{{ item }}</li>
  {% endfor %}
  </ul>
{% endfor %}
```


---

## Работа с [[dict]]

Можно перебирать словари:

```jinja2
{% for key, value in data.items() %}
  {{ key }}: {{ value }}
{% endfor %}
```


---

## Прерывание и продолжение

- `break` — выйти из цикла
    
- `continue` — перейти к следующей итерации

```jinja2
{% for num in numbers %}
  {% if num < 0 %}
    {% continue %}
  {% endif %}
  {{ num }}
  {% if num > 100 %}
    {% break %}
  {% endif %}
{% endfor %}
```


---

## Итог

- Цикл `for ... endfor` для списков, словарей и генераторов
    
- Объект `loop` даёт доступ к индексу, длине и флагам
    
- Есть поддержка `if` внутри цикла
    
- `else` для пустых коллекций
    
- Поддержка вложенности
    
- Управление циклом через `break` и `continue`