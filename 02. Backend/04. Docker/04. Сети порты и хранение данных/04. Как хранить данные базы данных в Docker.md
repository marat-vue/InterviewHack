# Как хранить данные базы данных в Docker?

> [!NOTE]
> Данные базы нельзя хранить только в writable layer контейнера. Для PostgreSQL, MySQL, MongoDB и других stateful-сервисов нужно использовать named volumes или внешнее managed-хранилище.

## Почему container filesystem не подходит?

Контейнер можно удалить:

```bash
docker rm db
```

Если данные лежали только внутри контейнера, они исчезнут вместе с его writable layer.

Для database это означает потерю данных.

## PostgreSQL с volume

```bash
docker run -d \
  --name db \
  -e POSTGRES_USER=app \
  -e POSTGRES_PASSWORD=secret \
  -e POSTGRES_DB=app \
  -v pgdata:/var/lib/postgresql/data \
  -p 5432:5432 \
  postgres:18
```

`pgdata` живет отдельно от container.

## Compose пример

```yaml
services:
  db:
    image: postgres:18
    environment:
      POSTGRES_USER: app
      POSTGRES_PASSWORD: secret
      POSTGRES_DB: app
    volumes:
      - pgdata:/var/lib/postgresql/data
    ports:
      - "5432:5432"

volumes:
  pgdata:
```

Если выполнить:

```bash
docker compose down
docker compose up -d
```

данные сохранятся.

Но:

```bash
docker compose down -v
```

удалит volumes, если они принадлежат Compose project.

## Backup

Для PostgreSQL:

```bash
docker exec db pg_dump -U app app > backup.sql
```

Restore:

```bash
docker exec -i db psql -U app app < backup.sql
```

В production backup должен быть регулярным и проверяемым.

## Dev vs production

В dev удобно держать Postgres в Docker volume.

В production часто используют:

- managed database;
- отдельный database server;
- volume на сервере;
- orchestrator storage;
- backup policy.

Docker не отменяет ответственность за backup, migration и monitoring.

## Что отвечать на собеседовании?

Данные базы в Docker нужно хранить вне контейнера: чаще всего в named volume или внешнем managed-хранилище. Контейнер disposable, его можно удалить и пересоздать. Volume переживает удаление контейнера, но его тоже можно удалить явно, поэтому для production нужны backup и осторожная работа с `docker compose down -v`.

## Частые ошибки

- Запускать database без volume.
- Делать `docker compose down -v` и терять dev database.
- Считать volume полноценным backup.
- Публиковать порт базы наружу в production без необходимости.
- Хранить пароль базы прямо в compose-файле production.
- Не проверять restore из backup.

## Мини-шпаргалка

- База stateful.
- Container disposable.
- Database data -> named volume.
- `down` сохраняет volume.
- `down -v` удаляет volume.
- Volume не заменяет backup.
