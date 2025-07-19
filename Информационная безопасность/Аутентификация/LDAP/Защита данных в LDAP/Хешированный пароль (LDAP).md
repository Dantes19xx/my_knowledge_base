#ИБ 

```
dn: uid=john,ou=People,dc=example,dc=com
userPassword: {SSHA}DkMTwBl+a/3DQTxCYEApdUtNXGgdUac3 
```

Вот возможные префиксы хеширования:

- `{SSHA}` — Salted SHA.
- `{SHA}` — SHA-1.
- `{MD5}` — MD5 (устаревший и небезопасный вариант).
- `{CRYPT}` — Unix crypt.
- `{BCRYPT}` — BCrypt.