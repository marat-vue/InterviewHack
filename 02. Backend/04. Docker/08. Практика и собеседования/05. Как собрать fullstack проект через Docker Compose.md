# Как собрать fullstack проект через Docker Compose?

> [!NOTE]
> Fullstack Compose-проект обычно состоит из frontend, backend, database, Redis и reverse proxy. В dev можно использовать hot reload и bind mounts, а в production - готовые images, минимум ports наружу и отдельные env/secrets.

## Пример структуры

```text
project/
  frontend/
    Dockerfile
  backend/
    Dockerfile
  nginx/
    nginx.conf
  compose.yaml
  .env.example
```

## Compose пример

```yaml
services:
  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/conf.d/default.conf:ro
    depends_on:
      - frontend
      - backend

  frontend:
    build:
      context: ./frontend
    expose:
      - "80"

  backend:
    build:
      context: ./backend
    environment:
      DATABASE_URL: postgres://app:secret@db:5432/app
      REDIS_URL: redis://redis:6379
    expose:
      - "3000"
    depends_on:
      db:
        condition: service_healthy
      redis:
        condition: service_started

  db:
    image: postgres:18
    environment:
      POSTGRES_USER: app
      POSTGRES_PASSWORD: secret
      POSTGRES_DB: app
    volumes:
      - pgdata:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U app -d app"]
      interval: 5s
      retries: 10

  redis:
    image: redis:8-alpine

volumes:
  pgdata:
```

## Nginx route example

```nginx
server {
  listen 80;

  location /api/ {
    proxy_pass http://backend:3000/;
  }

  location / {
    proxy_pass http://frontend:80;
  }
}
```

Nginx обращается к services по именам `backend` и `frontend`.

## Dev vs production

Dev:

- bind mounts;
- hot reload;
- published ports для frontend/backend/db;
- debug tools;
- простые local secrets.

Production:

- prebuilt images;
- no source bind mounts;
- минимум открытых ports;
- secrets не в git;
- healthchecks;
- restart policies;
- logs в stdout/stderr.

## Что отвечать на собеседовании?

Fullstack Docker Compose проект описывает каждый компонент как service: frontend, backend, database, Redis, Nginx. Services общаются по именам внутри docker network. Наружу обычно публикуется только Nginx или frontend/backend dev ports, база хранит данные в named volume, backend получает env с host `db` и `redis`, а готовность базы проверяется healthcheck.

## Частые ошибки

- Открывать наружу все services.
- Использовать `localhost` между containers.
- Не добавлять volume для базы.
- Смешивать dev и production настройки без profiles/override.
- Запускать migrations из каждой backend replica.
- Хранить secrets прямо в compose.yaml.

## Мини-шпаргалка

- Каждый компонент -> service.
- Между services -> DNS names.
- Наружу публикуй минимум ports.
- DB data -> volume.
- Dev -> bind mounts.
- Prod -> prebuilt images and secrets.
