# Что такое healthcheck?

> [!NOTE]
> Healthcheck - это проверка состояния контейнера. Она помогает понять, что процесс не просто запущен, а действительно готов принимать запросы: API отвечает на `/health`, база принимает соединения, Redis доступен.

## Почему running не значит ready?

Контейнер может быть в статусе running, но приложение еще не готово.

Примеры:

- PostgreSQL запускается, но еще не принимает подключения;
- backend стартовал, но миграции еще не завершены;
- API процесс жив, но завис на подключении к базе;
- Nginx запущен, но upstream недоступен.

## Dockerfile HEALTHCHECK

```dockerfile
HEALTHCHECK --interval=30s --timeout=3s --retries=3 \
  CMD wget -qO- http://localhost:3000/health || exit 1
```

Если команда возвращает `0`, container healthy. Если не `0`, проверка failed.

## Compose healthcheck

```yaml
services:
  api:
    build: .
    healthcheck:
      test: ["CMD", "wget", "-qO-", "http://localhost:3000/health"]
      interval: 10s
      timeout: 3s
      retries: 5
      start_period: 20s
```

Для PostgreSQL:

```yaml
services:
  db:
    image: postgres:18
    environment:
      POSTGRES_USER: app
      POSTGRES_PASSWORD: secret
      POSTGRES_DB: app
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U app -d app"]
      interval: 5s
      timeout: 3s
      retries: 10
```

## Healthcheck и depends_on

```yaml
services:
  api:
    build: .
    depends_on:
      db:
        condition: service_healthy

  db:
    image: postgres:18
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U app"]
      interval: 5s
      timeout: 3s
      retries: 10
```

Так `api` стартует после того, как `db` стала healthy.

## Что должен проверять /health?

Для простого API:

```text
GET /health -> 200 OK
```

Для production лучше различать:

- liveness: процесс жив;
- readiness: сервис готов принимать трафик;
- dependency health: база, Redis, внешние API.

## Что отвечать на собеседовании?

Healthcheck проверяет реальную готовность контейнера, а не только факт запущенного процесса. Он выполняет команду внутри контейнера и переводит container в состояния healthy или unhealthy. В Compose healthcheck часто используют вместе с `depends_on.condition: service_healthy`, чтобы сервисы стартовали после готовности зависимостей.

## Частые ошибки

- Считать running container готовым сервисом.
- Проверять только процесс, а не endpoint.
- Делать слишком тяжелый healthcheck.
- Ставить маленький timeout для медленно стартующей базы.
- Не учитывать, что приложение должно само переживать reconnect.

## Мини-шпаргалка

- Running не равно ready.
- Healthcheck возвращает exit code.
- `0` - healthy.
- Compose поддерживает `condition: service_healthy`.
- Для Postgres удобно `pg_isready`.
- Healthcheck не заменяет retry logic в приложении.
