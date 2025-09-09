#flask #python #фреймворки #flask_extensions 

# Flask-Migrate

## Что это
**Flask-Migrate** — расширение для Flask, упрощающее управление изменениями базы данных (миграциями).  
Работает поверх **SQLAlchemy** и **[[Alembic]]**.

---

## Зачем нужно
- Автоматизирует процесс изменения структуры БД.  
- Позволяет создавать, применять и откатывать миграции.  
- Удобно работать в команде, когда схема базы часто меняется.

---

## Основные команды

- Инициализация системы миграций:
  ```bash
  flask db init
  ```

- Создание новой миграции:
    
    `flask db migrate -m "Комментарий"`
    
- Применение миграций:
    
    `flask db upgrade`
    
- Откат к предыдущей версии:
    
    `flask db downgrade`

---

### Пример использования

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy
from flask_migrate import Migrate

app = Flask(__name__)
app.config["SQLALCHEMY_DATABASE_URI"] = "sqlite:///example.db"

db = SQLAlchemy(app)
migrate = Migrate(app, db)

class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(50))
```

Затем в консоли:

```bash
flask db init
flask db migrate -m "Создал таблицу User"
flask db upgrade
```

## В связке с другими инструментами

- **SQLAlchemy** — ORM, описывает модели и управляет взаимодействием с БД.
    
- **Alembic** — система миграций для SQLAlchemy.
    
- **Flask-Migrate** — обёртка для удобной интеграции Alembic во Flask.
    

---

## Полезно помнить

- Миграции хранятся в папке `migrations/`.
    
- После изменения моделей необходимо запускать `flask db migrate`.
    
- Не стоит редактировать миграции вручную, если это не крайняя необходимость.