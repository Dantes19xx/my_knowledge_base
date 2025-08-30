#flask #python #фреймворки #flask_extensions 

## Что это

**Flask-WTF** — расширение Flask, которое интегрирует библиотеку **WTForms** (Web Forms) во Flask.  
Оно упрощает работу с HTML-формами: создание, валидация, защита от [[CSRF]].

---

## Основные возможности

- **Удобное определение форм в виде Python-классов**
    
    - поля (`StringField`, `PasswordField`, `BooleanField` и др.)
        
    - валидаторы (`DataRequired`, `Email`, `Length`, `EqualTo`)
        
- **Валидация данных**
    
    - автоматическая проверка введённых данных при отправке формы
        
    - ошибки можно отображать прямо в шаблонах
        
- **CSRF защита**
    
    - встроенная защита от подделки межсайтовых запросов
        
- **Интеграция с [[Что такое Jinja2|Jinja2]]**
    
    - простая отрисовка полей (`{{ form.field() }}`)
        
- **Гибкость**
    
    - можно как использовать готовый рендеринг, так и полностью кастомизировать HTML
        

---

## Роль во Flask

- Делает работу с формами более **структурированной** и безопасной
    
- Экономит время на ручной валидации и защиту от CSRF
    
- Полезно для форм регистрации, логина, профиля, поиска и т.д.
    

---

## Типичный рабочий процесс

1. Настройка приложения:
```python
from flask_wtf import FlaskForm
from wtforms import StringField, PasswordField, SubmitField
from wtforms.validators import DataRequired

app.config["SECRET_KEY"] = "секретный_ключ"
```

2. Определение формы:
```python
class LoginForm(FlaskForm):
    username = StringField("Имя пользователя", validators=[DataRequired()])
    password = PasswordField("Пароль", validators=[DataRequired()])
    submit = SubmitField("Войти")
```

3. Использование во вьюхе:
```python
@app.route("/login", methods=["GET", "POST"])
def login():
    form = LoginForm()
    if form.validate_on_submit():
        return "Форма валидна!"
    return render_template("login.html", form=form)
```

4. В шаблоне (Jinja2):
```jinja2
<form method="POST">
    {{ form.hidden_tag() }}  {# CSRF-токен #}
    {{ form.username.label }} {{ form.username() }}
    {{ form.password.label }} {{ form.password() }}
    {{ form.submit() }}
</form>
```

## Особенности

- Требует `SECRET_KEY` в приложении (для CSRF)
    
- Расширяет WTForms, но оставляет возможность низкоуровневого контроля
    
- Легко комбинируется с [[Flask-Login]] (например, для форм регистрации/логина)
    

---

📌 **Итог**: Flask-WTF — это расширение для удобной и безопасной работы с формами во Flask. Оно объединяет WTForms + CSRF защиту + интеграцию с Jinja2.