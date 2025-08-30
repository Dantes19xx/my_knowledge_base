#flask #python #фреймворки #flask_extensions 

## Что это

**Flask-Mail** — это расширение Flask для отправки email-сообщений через SMTP.  
Оно интегрируется с приложением и позволяет удобно работать с письмами: текст, HTML, вложения.

---

## Основные возможности

- Отправка **текстовых и HTML-писем**
    
- Поддержка **вложений** (файлов, картинок)
    
- Работа через SMTP-серверы (Gmail, Яндекс, корпоративная почта и т.д.)
    
- Поддержка **асинхронной отправки** (через Celery/ThreadPool)
    
- Простая интеграция в Flask-приложение
    

---

## Роль во Flask

Flask сам по себе не умеет отправлять письма.  
Flask-Mail добавляет слой для:

- подтверждения email при регистрации,
    
- восстановления пароля,
    
- уведомлений пользователям,
    
- рассылок.
    

---

## Типичный рабочий процесс

1. Установка:
```bash
pip install Flask-Mail
```

2. Настройка:

```python
from flask import Flask
from flask_mail import Mail, Message

app = Flask(__name__)

app.config["MAIL_SERVER"] = "smtp.gmail.com"
app.config["MAIL_PORT"] = 587
app.config["MAIL_USE_TLS"] = True
app.config["MAIL_USERNAME"] = "your_email@gmail.com"
app.config["MAIL_PASSWORD"] = "your_password"

mail = Mail(app)
```

3. Отправка письма:
```python
@app.route("/send")
def send_mail():
    msg = Message(
        "Привет из Flask!",
        sender="your_email@gmail.com",
        recipients=["user@example.com"]
    )
    msg.body = "Это текстовое письмо."
    msg.html = "<b>Это HTML-письмо</b>"
    mail.send(msg)
    return "Письмо отправлено!"
```


---

## Особенности

- Для Gmail и других сервисов часто нужно включать **специальные пароли приложений** (иначе блокируется).
    
- Для продакшена лучше использовать **асинхронную отправку** (через Celery или `threading`), чтобы не блокировать запросы.
    
- Есть альтернативы: **Flask-Mailman**, **Flask-SendGrid** (подходит для API-провайдеров).