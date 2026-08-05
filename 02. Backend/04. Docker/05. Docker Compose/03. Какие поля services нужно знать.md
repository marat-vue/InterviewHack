# Какие поля services нужно знать?

> [!NOTE]
> В Compose service чаще всего описывают через `image`, `build`, `container_name`, `ports`, `expose`, `environment`, `env_file`, `volumes`, `depends_on`, `healthcheck`, `restart`, `command`, `entrypoint`, `working_dir`, `networks` и `profiles`.

## image

```yaml
services:
  redis:
    image: redis:8-alpine
```

Используется готовый image из registry или локальный image.

## build

```yaml
services:
  api:
    build:
      context: .
      dockerfile: Dockerfile
      target: runner
```

Compose соберет image из Dockerfile.

## ports

```yaml
ports:
  - "3000:3000"
```

Публикует container port на host.

## expose

```yaml
expose:
  - "3000"
```

Открывает порт для других services в docker-сети, но не публикует его на host.

## environment

```yaml
environment:
  NODE_ENV: development
  PORT: 3000
```

Передает env в container.

## env_file

```yaml
env_file:
  - .env
```

Подгружает переменные из файла.

## volumes

```yaml
volumes:
  - .:/app
  - pgdata:/var/lib/postgresql/data
```

Монтирует bind mounts, named volumes или anonymous volumes.

## depends_on

```yaml
depends_on:
  - db
```

Управляет порядком запуска и остановки. Для ожидания readiness нужен healthcheck и condition.

## healthcheck

```yaml
healthcheck:
  test: ["CMD", "wget", "-qO-", "http://localhost:3000/health"]
  interval: 10s
  timeout: 3s
  retries: 5
```

Проверяет состояние service container.

## restart

```yaml
restart: unless-stopped
```

Популярные варианты:

- `no`;
- `always`;
- `on-failure`;
- `unless-stopped`.

## command и entrypoint

```yaml
command: npm run dev
```

Переопределяет `CMD` image.

```yaml
entrypoint: ["docker-entrypoint.sh"]
```

Переопределяет `ENTRYPOINT`.

## profiles

```yaml
profiles:
  - debug
```

Service запустится только при указанном profile:

```bash
docker compose --profile debug up
```

## Что отвечать на собеседовании?

В `services` нужно уверенно знать поля `image` и `build`, публикацию портов через `ports`, env через `environment` и `env_file`, storage через `volumes`, связи через `networks`, порядок запуска через `depends_on`, readiness через `healthcheck`, restart policy, а также `command`, `entrypoint`, `profiles`.

## Частые ошибки

- Использовать `container_name` везде и ломать масштабирование service.
- Думать, что `depends_on` без healthcheck ждет готовности приложения.
- Путать `ports` и `expose`.
- Хранить sensitive values прямо в `environment`.
- Переопределять `command` и случайно отключать правильный startup.
- Не понимать, что `deploy` в обычном local Compose может игнорироваться.

## Мини-шпаргалка

- `image` - готовый image.
- `build` - сборка.
- `ports` - наружу на host.
- `environment` - env.
- `volumes` - файлы и данные.
- `depends_on` - порядок.
- `healthcheck` - готовность.
- `profiles` - опциональные services.
