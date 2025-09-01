
#flask #python #фреймворки #flask_extensions 

1. **База данных указывается в конфигурации Flask**  
В `config.py` или прямо в коде задаётся строка подключения:

```python
app.config["SQLALCHEMY_DATABASE_URI"] = "postgresql://user:password@localhost:5432/mydb"
```
👉 Вот эта строка говорит: _"работаем с такой-то базой"_.

2. **SQLAlchemy получает эту строку**  
Когда ты создаёшь объект:

```python
db = SQLAlchemy(app)
```
он сохраняет подключение к базе.

3. **[[Flask-Migrate]]/[[Alembic]] берёт подключение через SQLAlchemy**  
В файле `migrations/env.py` есть важный кусок:
```python
from app import db
target_metadata = db.metadata
```

И чуть ниже — функция, которая подключается к базе через `db.engine`:
```python
connectable = db.engine
with connectable.connect() as connection:
    context.configure(connection=connection, target_metadata=target_metadata)
```

3. 👉 Это значит: Alembic не сам хранит данные о базе, а использует `db.engine`, который уже знает строку подключения из `SQLALCHEMY_DATABASE_URI`.
    

---

4. **Команда `flask db upgrade`**  
    Когда ты выполняешь `flask db upgrade`, Flask-Migrate:
    
    - импортирует приложение
        
    - инициализирует `db` с конфигом
        
    - берёт `db.engine` и применяет миграции к базе, указанной в `SQLALCHEMY_DATABASE_URI`.