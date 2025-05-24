Базы данных, кэш, очереди и другие сервисы — это **внешние ресурсы**, подключаемые по URL из конфигурации. Приложение не должно зависеть от их местоположения — их можно свободно менять без изменения кода.

|Сервис|Переменная окружения|Пример значения|
|---|---|---|
|PostgreSQL|`DATABASE_URL`|`postgres://user:pass@localhost:5432/db`|
|Redis|`REDIS_URL`|`redis://localhost:6379/0`|
|RabbitMQ|`AMQP_URL`|`amqp://guest:guest@localhost:5672/`|
|AWS S3|`S3_BUCKET_URL`|`https://s3.amazonaws.com/my-bucket`|
|SMTP Server|`SMTP_HOST`|`smtp.mailtrap.io`|

