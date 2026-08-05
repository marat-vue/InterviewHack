# Как устроен compose.yaml?

> [!NOTE]
> `compose.yaml` описывает приложение как набор services, networks, volumes, configs и secrets. Главный раздел - `services`, где задают image или build, ports, environment, volumes, depends_on, healthcheck и другие параметры контейнеров.

## Базовая структура

```yaml
services:
  api:
    build: .
    ports:
      - "3000:3000"
    environment:
      NODE_ENV: development

  db:
    image: postgres:18
    environment:
      POSTGRES_USER: app
      POSTGRES_PASSWORD: secret
      POSTGRES_DB: app
    volumes:
      - pgdata:/var/lib/postgresql/data

volumes:
  pgdata:
```

## services

`services` - обязательный основной раздел.

Каждый ключ внутри `services` - имя service:

```yaml
services:
  api:
  db:
  redis:
```

Имена services становятся DNS-именами внутри сети Compose.

## image vs build

Готовый image:

```yaml
services:
  redis:
    image: redis:8-alpine
```

Сборка из Dockerfile:

```yaml
services:
  api:
    build:
      context: .
      dockerfile: Dockerfile
```

Можно указать и `build`, и `image`: Compose соберет image и присвоит ему имя.

## environment и env_file

```yaml
environment:
  NODE_ENV: development
  DATABASE_URL: postgres://app:secret@db:5432/app
```

Или:

```yaml
env_file:
  - .env
```

Важно: `.env` для подстановки переменных Compose и `env_file` для переменных контейнера - связанные, но не полностью одинаковые механизмы.

## ports и volumes

```yaml
ports:
  - "3000:3000"

volumes:
  - .:/app
  - pgdata:/var/lib/postgresql/data
```

`ports` публикует container port на host.

`volumes` подключает storage.

## networks

```yaml
services:
  api:
    networks:
      - backend
  db:
    networks:
      - backend

networks:
  backend:
```

Если networks не указаны, Compose создает default network.

## Что отвечать на собеседовании?

`compose.yaml` состоит из top-level sections, главная из которых `services`. В services описывают контейнеры: `image` или `build`, `ports`, `environment`, `env_file`, `volumes`, `depends_on`, `healthcheck`, `networks`. Top-level `volumes` и `networks` объявляют именованные ресурсы, которые затем подключаются к services.

## Частые ошибки

- Путать `image` и `build`.
- Ожидать, что `depends_on` всегда ждет готовности базы.
- Класть secrets прямо в YAML.
- Публиковать внутренние services через `ports`.
- Не объявлять named volume в top-level `volumes`.
- Путать `.env` Compose substitution и `env_file`.

## Мини-шпаргалка

- `services` - контейнеры приложения.
- `image` - готовый образ.
- `build` - собрать image.
- `ports` - host:container.
- `environment` - env внутри container.
- `volumes` - storage.
- `networks` - связь services.
