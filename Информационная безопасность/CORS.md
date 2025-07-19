#ИБ 

# CORS (Cross-Origin Resource Sharing)

## Что такое CORS

**CORS** — это механизм безопасности браузера, который регулирует доступ к ресурсам между разными источниками (доменами, портами, протоколами).

Он используется для защиты пользователей от небезопасных запросов из одного источника (например, с сайта `evil.com`) к ресурсам другого (например, `api.bank.com`).

---

## Пример ситуации

Фронтенд на `http://localhost:3000` хочет сделать запрос к API на `http://localhost:8000`. Это считается **междоменным запросом**.

Если сервер не разрешает CORS, браузер блокирует такой запрос.

---

## Как работает

### 1. **Простой запрос** (simple request)

Браузер отправляет обычный HTTP-запрос (например, `GET`, `POST` с `application/x-www-form-urlencoded`) и автоматически проверяет ответ на наличие CORS-заголовков:

```http
Access-Control-Allow-Origin: http://localhost:3000
```

### 2. **Предварительный запрос** (preflight request)

Если запрос содержит нестандартные заголовки, методы (`PUT`, `DELETE`, `Content-Type: application/json` и др.), то сначала отправляется **OPTIONS-запрос**:

```http
OPTIONS /api/data HTTP/1.1 
Origin: http://localhost:3000 Access-Control-Request-Method: POST 
Access-Control-Request-Headers: Content-Type
```


Если сервер отвечает с допустимыми заголовками, основной запрос выполняется.


---

## Основные заголовки CORS

|Заголовок|Назначение|
|---|---|
|`Access-Control-Allow-Origin`|Разрешённый источник (или `*`)|
|`Access-Control-Allow-Methods`|Разрешённые HTTP-методы|
|`Access-Control-Allow-Headers`|Разрешённые заголовки запроса|
|`Access-Control-Allow-Credentials`|Разрешение на использование cookie и авторизации|
|`Access-Control-Max-Age`|Время кэширования preflight-запроса|

## Безопасность

- Никогда не ставь `Access-Control-Allow-Origin: *` вместе с `Allow-Credentials: true` — это **уязвимость**.
    
- CORS — не механизм аутентификации или авторизации. Он лишь ограничивает доступ на стороне **браузера**.