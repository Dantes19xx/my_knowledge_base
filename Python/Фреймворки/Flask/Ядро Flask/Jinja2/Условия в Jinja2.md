#jinja2 #шаблонизатор 

## Основы
Для ветвления в Jinja2 используется конструкция `{% if %}`:

```jinja2
{% if user %}
  Привет, {{ user.name }}!
{% endif %}
```


---
## Полная форма

```jinja2
{% if balance > 0 %}
    У вас положительный баланс
{% elif balance == 0 %}
    Баланс пустой
{% else %}
    Баланс отрицательный
{% endif %}
```


---

## Логические операторы

В условиях можно использовать:

- `and`
    
- `or`
    
- `not`
    

Пример:
```jinja2
{% if user.is_active and not user.is_banned %}
    Добро пожаловать!
{% endif %}
```

---
## Проверка существования

- `is defined` — переменная существует
    
- `is not defined` — переменная не существует

```jinja2
{% if promo_code is defined %}
    Ваш промокод: {{ promo_code }}
{% endif %}
```


---

## Проверка пустоты

- `is none` — значение `None`
    
- `is not none` — значение задано
    
- `if variable` — проверка truthy

```jinja2
{% if items %}
    У вас есть товары
{% else %}
    Корзина пуста
{% endif %}
```


---

## Тесты (tests)

Jinja2 поддерживает дополнительные проверки через `is`:

```jinja2
{% if value is string %}
    Это строка
{% endif %}

{% if list_var is iterable %}
    Можно перебирать
{% endif %}
```


---

# Резюме

- Используются блоки `{% if %}`, `{% elif %}`, `{% else %}`.
    
- Поддерживаются логические операторы (`and`, `or`, `not`).
    
- Проверки: `is defined`, `is none`, типы (`is string`, `is iterable` и др.).
    
- Условия можно вкладывать друг в друга.