# Как запускать migrations и seed в Docker?

> [!NOTE]
> Миграции в Docker можно запускать вручную через `docker compose exec`, отдельным one-off сервисом или отдельным CI/CD шагом. В production важно не запускать миграции хаотично из каждой реплики backend.

## Ручной запуск в dev

```bash
docker compose exec api npx prisma migrate dev
docker compose exec api npx prisma db seed
```

Подходит для локальной разработки.

## One-off command

```bash
docker compose run --rm api npx prisma migrate deploy
```

`run --rm` создает одноразовый container для команды и удаляет его после завершения.

## Отдельный service для migrations

```yaml
services:
  migrate:
    build: .
    command: npx prisma migrate deploy
    env_file:
      - .env
    depends_on:
      db:
        condition: service_healthy

  api:
    build: .
    command: node dist/main.js
    depends_on:
      migrate:
        condition: service_completed_successfully
```

Так API стартует после успешного завершения migration service.

## Почему не всегда в entrypoint?

Иногда делают:

```dockerfile
CMD ["sh", "-c", "npx prisma migrate deploy && node dist/main.js"]
```

Для маленького pet-проекта это может быть терпимо, но в production опасно:

- несколько replicas могут запустить миграции одновременно;
- приложение стартует медленно;
- migration failure ломает container startup;
- сложнее контролировать rollback;
- нет отдельной видимости CI/CD шага.

## Production-подход

Частый вариант:

```text
build image -> push image -> run migrations once -> deploy app
```

Миграции запускают:

- отдельным pipeline job;
- one-off container;
- release command;
- migration service с гарантиями single-run.

## Seed

Seed - это заполнение начальными или тестовыми данными.

Dev:

```bash
docker compose exec api npm run seed
```

Production seed должен быть осторожным:

- idempotent;
- не удалять реальные данные;
- не запускаться случайно;
- иметь проверку окружения.

## Что отвечать на собеседовании?

Миграции в Docker можно запускать вручную, one-off командой или отдельным service. В dev это часто `docker compose exec api npx prisma migrate dev`, а в production лучше отдельный controlled step: `migrate deploy` один раз перед запуском приложения. Не стоит запускать миграции из каждой replica backend без контроля.

## Частые ошибки

- Запускать migrations одновременно из нескольких containers.
- Использовать dev-команды миграций в production.
- Не ждать readiness базы.
- Запускать seed в production случайно.
- Не делать migrations idempotent/controlled.
- Хранить DATABASE_URL с `localhost` внутри container.

## Мини-шпаргалка

- Dev: `docker compose exec api ...`.
- One-off: `docker compose run --rm api ...`.
- Production: migrations отдельным шагом.
- `depends_on + healthcheck` для базы.
- Seed должен быть безопасным.
- Не запускай migrations из каждой replica.
