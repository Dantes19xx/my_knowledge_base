#flask #python #фреймворки #flask_extensions 

## 1. Создаёшь или меняешь модель

Например, добавляешь новый класс или поле в `models.py`:

```python
class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(50))

# добавим поле
    email = db.Column(db.String(120), unique=True, nullable=False)
```

## 2. Генерация миграции

Запускаешь команду:

```bash
flask db migrate -m "Добавил поле email в User"
```

👉 Это создаст новый файл миграции в папке `migrations/versions/`.  
Там будет SQL-код, который добавляет новый столбец.

---

## 3. Применение миграции

Выполняешь:

```bash
flask db upgrade
```

👉 [[Flask-Migrate]] применит изменения к БД (например, добавит новый столбец).

---

## 4. Проверка

В БД появится новое поле или таблица.  
Можно проверить через `sqlite3`, `psql` или клиент типа DBeaver.

---

## 5. Если ошибся

Можно откатиться:
```bash
flask db downgrade
```

---

# ⚡ Полезные моменты

- Всегда пиши `-m "комментарий"` при `migrate`, чтобы помнить что за изменения.
    
- После редактирования моделей **никогда не меняй вручную схему в базе** — только через миграции.
    
- Миграции хранятся в Git, чтобы вся команда могла их применять.
    
- Flask-Migrate использует [[Alembic]] → в `migrations/versions/` лежит история изменений БД.
    

---

👉 То есть:  
**меняешь модели → `flask db migrate` → `flask db upgrade` → база обновляется**.