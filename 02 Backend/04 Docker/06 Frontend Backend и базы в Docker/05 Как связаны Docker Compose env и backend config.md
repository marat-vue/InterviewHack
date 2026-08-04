# Как связаны Docker Compose env и backend config?

> [!NOTE]
> Compose передает переменные окружения в контейнер через `environment` и `env_file`, а backend читает их через `process.env` или config-модуль. Важно различать env для Compose-подстановки, env внутри контейнера и публичные frontend-переменные.

## environment

```yaml
services:
  api:
    environment:
      NODE_ENV: production
      PORT: 3000
      DATABASE_URL: postgres://app:secret@db:5432/app
```

Эти переменные будут доступны внутри container:

```ts
const databaseUrl = process.env.DATABASE_URL
```

## env_file

```yaml
services:
  api:
    env_file:
      - .env
```

`.env`:

```env
PORT=3000
DATABASE_URL=postgres://app:secret@db:5432/app
JWT_SECRET=dev-secret
```

Так удобно для локальной разработки.

## Compose variable substitution

Compose сам может подставлять переменные:

```yaml
services:
  api:
    image: my-api:${APP_VERSION}
```

Значение `APP_VERSION` берется из shell environment или `.env` рядом с compose-файлом.

Это не то же самое, что `env_file` внутри контейнера.

## Важное различие

```text
.env for Compose substitution -> влияет на YAML
env_file -> передает env в container
environment -> передает env в container
```

Один и тот же `.env` можно использовать для обоих сценариев, но смысл разный.

## Frontend env

В frontend-проектах env часто встраивается в bundle во время build.

Vite:

```text
VITE_API_URL
```

Next.js:

```text
NEXT_PUBLIC_API_URL
```

Все public-переменные видны пользователю в браузере. Секреты туда класть нельзя.

## Что отвечать на собеседовании?

Compose передает env в container через `environment` и `env_file`. Backend читает эти значения из `process.env` или config layer. Нужно отличать переменные, которые Compose использует для подстановки в YAML, от переменных, которые реально попадают внутрь container. Для frontend public env встраиваются в bundle и не должны содержать secrets.

## Частые ошибки

- Путать `.env` Compose и `env_file`.
- Использовать `localhost` в `DATABASE_URL` вместо service name.
- Класть secrets в frontend public env.
- Думать, что изменение env всегда применится без пересоздания container.
- Хранить production secrets в git.
- Не валидировать env на старте backend.

## Мини-шпаргалка

- `environment` - env прямо в YAML.
- `env_file` - env из файла.
- `.env` рядом с Compose может подставлять значения в YAML.
- Backend читает `process.env`.
- Public frontend env не секретны.
- Внутри Docker service host - имя service.
