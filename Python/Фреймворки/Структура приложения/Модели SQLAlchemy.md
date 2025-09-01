#flask #web #ахитектура_по 

# Что такое модели SQLAlchemy

SQLAlchemy — это ORM (**Object Relational Mapper**) для Python.  
Она позволяет работать с базой данных **через Python-классы и объекты**, а не вручную писать SQL-запросы.

**Модель** в SQLAlchemy = Python-класс, который описывает таблицу в базе данных.  
Каждый объект этого класса = строка в таблице.


---
### Базовый пример модели

```python
from flask_sqlalchemy import SQLAlchemy

db = SQLAlchemy()

class User(db.Model):  # модель = таблица "user"
    id = db.Column(db.Integer, primary_key=True)   # столбец "id"
    username = db.Column(db.String(50), unique=True, nullable=False)  # столбец "username"
    email = db.Column(db.String(120), unique=True, nullable=False)    # столбец "email"

    def __repr__(self):
        return f"<User {self.username}>"
```

🔹 Здесь:

- `User` → таблица `user` в БД (по умолчанию имя берётся от класса, можно задать вручную `__tablename__ = "users"`)
    
- `id`, `username`, `email` → столбцы
    
- объект `User(username="dmitriy", email="d@ex.com")` → строка в таблице


---

### Добавление и запрос данных

```python
# Создать пользователя
user = User(username="dmitriy", email="d@ex.com")
db.session.add(user)
db.session.commit()

# Найти всех пользователей
users = User.query.all()

# Найти одного по условию
u = User.query.filter_by(username="dmitriy").first()

# Обновить
u.email = "new@ex.com"
db.session.commit()

# Удалить
db.session.delete(u)
db.session.commit()
```


---
## Связи между моделями

### One-to-Many (Один ко многим)

```python
class Post(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    title = db.Column(db.String(100))
    user_id = db.Column(db.Integer, db.ForeignKey("user.id"))  # внешний ключ

    user = db.relationship("User", backref="posts")
```

Теперь:

```python
user = User.query.first() 
print(user.posts)  # список постов пользователя
```

### Many-to-Many (Многие ко многим)

```python
association = db.Table(
    "association",
    db.Column("user_id", db.Integer, db.ForeignKey("user.id")),
    db.Column("group_id", db.Integer, db.ForeignKey("group.id"))
)

class Group(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(50))

class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(50))
    groups = db.relationship("Group", secondary=association, backref="users")
```

## 📌 Как думать о моделях

- **Класс** = таблица
    
- **Атрибут** (`db.Column`) = столбец
    
- **Экземпляр класса** = строка
    
- **Методы ORM (`query`, `filter_by`, `add`, `commit`)** = SQL-запросы, но в Python-стиле