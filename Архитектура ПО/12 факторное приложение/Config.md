Хранить конфигурацию (**ключи, строки подключения, токены**) в **переменных окружения**, а не в коде. Это обеспечивает безопасность, гибкость и независимость от среды. Использовать `.env`-файлы локально и не включать их в репозиторий.

`import os`
`DATABASE_URL = os.getenv("DATABASE_URL")`

`.env`
`DATABASE_URL=postgres://user:pass@host/db`
`SECRET_KEY=supersecret`

`.docker-compose.yml`
`environment:`
  - `DATABASE_URL=${DATABASE_URL}`
  - `SECRET_KEY=${SECRET_KEY}`


#проектирование 