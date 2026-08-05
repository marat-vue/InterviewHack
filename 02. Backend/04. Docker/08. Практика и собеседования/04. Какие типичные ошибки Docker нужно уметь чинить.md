# Какие типичные ошибки Docker нужно уметь чинить?

> [!NOTE]
> Самые частые Docker-проблемы: контейнер сразу падает, порт недоступен, backend не видит базу, volume затирает файлы, env не попали внутрь, build cache ведет себя неожиданно, image слишком большой или нет прав на запись.

## Container exits immediately

Проверка:

```bash
docker ps -a
docker logs app
```

Причины:

- главный процесс завершился;
- неправильный `CMD`;
- missing file;
- приложение упало из-за env;
- не установлены dependencies.

## Port is not reachable

Проверка:

```bash
docker ps
docker inspect app
```

Причины:

- нет `-p` или `ports`;
- перепутан `host:container`;
- приложение слушает `127.0.0.1`, а нужно `0.0.0.0`;
- host port занят;
- firewall/proxy.

## Backend cannot connect to database

Плохо:

```text
DATABASE_URL=postgres://app:secret@localhost:5432/app
```

Внутри Compose правильно:

```text
DATABASE_URL=postgres://app:secret@db:5432/app
```

Также проверь:

- db service name;
- network;
- healthcheck;
- credentials;
- database name;
- migrations.

## node_modules исчезают или конфликтуют

Проблема:

```yaml
volumes:
  - .:/app
```

Host bind mount может затереть `/app/node_modules` внутри container.

Частое dev-решение:

```yaml
volumes:
  - .:/app
  - /app/node_modules
```

## Env не применились

Проверка:

```bash
docker compose exec api printenv
```

Причины:

- переменная есть в `.env`, но не передана в container;
- перепутаны `.env` и `env_file`;
- container не пересоздан;
- значение переопределено в `environment`;
- frontend env зашит на build-time.

## Permission denied

Причины:

- container работает под non-root user;
- volume принадлежит другому UID/GID;
- bind mount с host имеет неподходящие права;
- приложение пишет в директорию, где нет прав.

Решения зависят от проекта: правильно выбрать рабочую директорию, владельца файлов и пользователя.

## Что отвечать на собеседовании?

Типичные Docker-ошибки чинятся диагностикой по слоям: `ps -a` и `logs` для падений, `inspect` для ports/env/mounts/network, `exec` для проверки внутри container. Самые частые причины - неправильный port mapping, `localhost` вместо service name, отсутствующий volume, неверный env, конфликт bind mount с `node_modules` и permission issues.

## Частые ошибки

- Пересобирать image вслепую без logs.
- Не проверять переменные внутри container.
- Не различать build-time и runtime.
- Удалять volumes в попытке "починить".
- Менять container вручную вместо Dockerfile.
- Не смотреть health status.

## Мини-шпаргалка

- Exited -> `docker logs`.
- Port -> `ports`, `0.0.0.0`, busy host port.
- DB -> service name, not localhost.
- Env -> `printenv`.
- Files -> mounts and permissions.
- Build -> context/cache/dockerignore.
