#flask #python #фреймворки #flask_extensions

## Базы данных

- **[[Flask-SQLAlchemy]]** — упрощённая интеграция SQLAlchemy (ORM).
    
- **Flask-Migrate** — миграции БД на базе Alembic.
    
- **Flask-MongoEngine** — работа с MongoDB через MongoEngine.
    
- **Flask-Peewee** — интеграция с ORM Peewee.
    

## Аутентификация и безопасность

- **[[Flask-Login]]** — управление пользователями, логин/логаут, сессии.
    
- **Flask-Security** — расширенный пакет (логин, роли, права, пароли).
    
- **Flask-Principal** — система ролей и авторизации.
    
- **Flask-JWT-Extended** — работа с JWT-токенами.
    
- **Flask-OAuthlib / Authlib** — [[OAuth 2.0]], OpenID Connect.
    

## Формы и валидация

- **[[Flask-WTF]]** — обёртка над WTForms для работы с формами.
    
- **Flask-Inputs** — валидация входных данных (например, JSON).
    

## Интернационализация и локализация

- **[[Flask-Babel]]** — [[i18n и l10n]], поддержка перевода и дат.
    
- **Flask-BabelEx** — расширенный Babel (совместим с Flask-Security).
    

## API и сериализация

- **[[Flask-RESTful]]** — создание REST API.
    
- **Flask-RESTX** — расширение RESTful с документацией Swagger.
    
- **Flask-API** — минималистичный REST API toolkit.
    
- **Flask-Smorest** — REST + Marshmallow + OpenAPI.
    

## UI и админка

- **Flask-Admin** — автогенерируемая админка для БД.
    
- **[[Flask-Breadcrumbs]]** — хлебные крошки в навигации.
    
- **Flask-Menu** — система меню для навигации.
    

## Асинхронность и фоновые задачи

- **Flask-CeleryExt** — интеграция с Celery.
    
- **[[Flask-SocketIO]]** — работа с WebSocket.
    
- **Flask-Executor** — запуск фоновых задач (thread/process pool).
    

## Тестирование

- **Flask-Testing** — утилиты для unit-тестов.
    
- **pytest-flask** — плагины для pytest.
    

## Разное

- **Flask-Caching** — кэширование ([[Redis]], Memcached и др.).
    
- **[[Flask-Mail]]** — отправка email.
    
- **Flask-Uploads** — загрузка файлов.
    
- **Flask-Limiter** — ограничение запросов (rate limiting).
    
- **[[Flask-Session]]** — серверные сессии ([[Redis]], Memcached, SQL).
    
- **Flask-DebugToolbar** — панель разработчика (как Django Debug Toolbar).

- Flask-Redis - то расширение Flask, которое облегчает интеграцию **[[Redis]]** в приложение.  
Оно предоставляет удобный доступ к Redis-клиенту напрямую через объект приложения Flask.
    

---

📌 **Итог**:  
Расширения Flask — это «надстройки», которые делают его ближе к «большому фреймворку» вроде Django. Базовый Flask даёт только каркас, а расширения добавляют ORM, миграции, формы, авторизацию, REST API, кэширование и админку.