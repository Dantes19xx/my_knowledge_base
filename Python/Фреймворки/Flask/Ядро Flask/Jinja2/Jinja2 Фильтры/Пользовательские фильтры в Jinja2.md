#jinja2 #шаблонизатор

## Как добавить свой фильтр

### 1. Определяем функцию в Python

Фильтр — это обычная функция, принимающая значение и возвращающая преобразованный результат:

```python
# jinja_filters.py
def date_or_none(value):
    if value is None:
        return "-"
    return value.strftime("%Y-%m-%d")
```

### 2. Регистрируем фильтр в приложении Flask

У объекта Flask (`app`) есть свойство `jinja_env`, которое хранит окружение Jinja и все доступные фильтры.  
Добавление фильтра:

```python
from .jinja_filters import date_or_none

app.jinja_env.filters["date_or_none"] = date_or_none
```

Или регистрация сразу нескольких:

```python
from .jinja_filters import (
    date_or_none,
    time_or_none,
    get_date_from_analyze_dict,
)

custom_filters = {
    "date_or_none": date_or_none,
    "time_or_none": time_or_none,
    "get_date_from_analyze_dict": get_date_from_analyze_dict,
}

app.jinja_env.filters.update(custom_filters)
```

## Использование в шаблонах

Теперь в Jinja-шаблоне можно применять фильтр:

```jinja2
<td>{{ user.birth_date | date_or_none }}</td>
```

Если `user.birth_date = None` → отобразится `"-"`  
Если `user.birth_date = datetime(2025, 8, 15)` → отобразится `"2025-08-15"`

---

## Важные моменты

- `app.jinja_env` создаётся **по умолчанию** при инициализации Flask-приложения.
    
- В `app.jinja_env.filters` уже есть встроенные фильтры (например `upper`, `lower`).
    
- Добавленные вручную функции становятся доступными во всех шаблонах.
    

---

## Резюме

1. Создаёшь функцию в Python (`jinja_filters.py`).
    
2. Регистрируешь её через `app.jinja_env.filters["имя"] = функция`.
    
3. Используешь в шаблонах через `|`.