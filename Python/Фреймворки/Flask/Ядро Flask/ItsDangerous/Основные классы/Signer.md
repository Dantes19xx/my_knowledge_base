#flask #python #фреймворки 

Класс `Signer` занимается **криптографическим подписыванием строк**.  
Он не шифрует данные, а лишь добавляет **подпись (HMAC)**, чтобы проверить целостность.

---

## Пример использования

```python
from itsdangerous import Signer

# создаём объект Signer с секретным ключом
signer = Signer(b"my-secret-key")

# Подписывание строки
signed = signer.sign(b"hello-world")
print(signed)  
# b'hello-world.yFFgzaiVK7kHXcXWwTvHbFICd1o'

# Проверка подписи (верификация)
original = signer.unsign(signed)
print(original)  
# b'hello-world'
```

Если кто-то попытается изменить строку или подпись, вызов `unsign` вызовет ошибку `BadSignature`.


---

## Важные параметры

```python
signer = Signer(
    secret_key=b"secret",       # секретный ключ
    salt=b"my-salt",            # "соль" для изменения подписи
    sep=b".",                   # разделитель между данными и подписью (по умолчанию ".")
    key_derivation="hmac",      # способ derivation: "hmac", "concat", "django-concat", "django-salted"
    digest_method=None          # метод хэширования (по умолчанию SHA1)
)
```


---

## Типичный сценарий применения

- **Flask cookies** → Flask подписывает session-cookie через `itsdangerous`.
    
- **Reset-password ссылки** → токен с ID пользователя + подпись.
    
- **[[CSRF]] токены** → хранятся с подписью, чтобы нельзя было подделать.