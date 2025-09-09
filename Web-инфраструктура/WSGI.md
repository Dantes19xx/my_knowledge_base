#web

## Что такое WSGI

**WSGI (Web Server Gateway Interface)** — это спецификация интерфейса между веб-сервером и Python-приложением.  
Позволяет серверам взаимодействовать с Python-кодом без привязки к конкретному фреймворку или серверу.

Пример: `Gunicorn` (сервер) может запускать приложение на `Flask` или `Django`, если они реализуют WSGI.

## Зачем нужен WSGI

- Стандартизует способ связи между сервером и Python-приложением.
- Позволяет переиспользовать код с разными серверами и фреймворками.
- Является основой большинства классических Python веб-приложений.

## Архитектура WSGI

WSGI-приложение — это просто **функция**, которая принимает два аргумента:

```python
def application(environ, start_response):
    start_response("200 OK", [("Content-Type", "text/plain")])
    return [b"Hello, World!"]
```


---

### Аргументы:

- `environ`: словарь с данными запроса (HTTP-заголовки, путь, метод и т.д.)
    
- `start_response`: функция, которой передаётся статус ответа и заголовки


---

### Минималистичный пример WSGI-приложения

```python
from wsgiref.simple_server import make_server

def app(environ, start_response):
    start_response("200 OK", [("Content-Type", "text/plain")])
    return [b"WSGI Hello World"]

if __name__ == "__main__":
    server = make_server("", 8000, app)
    print("Serving on port 8000...")
    server.serve_forever()
```


---

## Популярные WSGI-серверы

|Сервер|Особенности|
|---|---|
|Gunicorn|Простой, многопроцессный|
|uWSGI|Гибкий, продвинутый, мощный|
|mod_wsgi|Используется с Apache|
|waitress|Надёжен, кроссплатформенный|

## WSGI vs ASGI

|Характеристика|WSGI|ASGI|
|---|---|---|
|Тип|Синхронный|Асинхронный + синхронный|
|Подходит для|Классических веб-приложений|WebSocket, HTTP/2, asyncio|
|Примеры|Flask, Django (до 3.x)|FastAPI, Starlette, Django 3.0+|

## Когда использовать

- Подходит для **простых, синхронных веб-приложений**
    
- Если не требуется WebSocket или асинхронная обработка