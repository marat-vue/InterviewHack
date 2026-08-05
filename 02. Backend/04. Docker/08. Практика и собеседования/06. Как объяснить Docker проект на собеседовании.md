# Как объяснить Docker проект на собеседовании?

> [!NOTE]
> Docker-проект на собеседовании лучше объяснять как систему: какие services есть, какие images собираются, как они связаны через networks, где хранятся данные, какие env нужны, как запускаются migrations, как устроен dev и production сценарий.

## Хорошая структура ответа

1. Что за приложение.
2. Какие services есть.
3. Какие Dockerfile собирают images.
4. Как services общаются.
5. Где хранятся данные.
6. Какие ports открыты наружу.
7. Как передаются env/secrets.
8. Как запускаются migrations.
9. Как смотреть logs и debug.
10. Чем dev отличается от production.

## Пример ответа

```text
У нас есть backend API, frontend, PostgreSQL и Redis.
Backend собирается из Dockerfile через multi-stage build.
Postgres и Redis берутся из official images.
Compose создает общую network, поэтому backend подключается к db:5432 и redis:6379.
Данные Postgres лежат в named volume pgdata.
Наружу открыт только порт приложения или Nginx, база не публикуется в production.
Env передаются на runtime, secrets не попадают в image.
Миграции запускаются отдельным one-off step перед стартом API.
Для отладки используем compose logs, ps, exec и inspect.
```

## Что подчеркнуть

- Docker нужен не "чтобы модно", а для воспроизводимого окружения.
- Dockerfile описывает image.
- Compose описывает multi-service topology.
- Containers disposable.
- State хранится во volumes/managed services.
- Secrets не запекаются в image.
- Production image отличается от dev container.

## Какие вопросы могут задать дальше?

- Почему `db`, а не `localhost`?
- Что будет после `docker compose down -v`?
- Как уменьшить image?
- Почему нужен `.dockerignore`?
- Чем `RUN` отличается от `CMD`?
- Как проверить, почему container упал?
- Как избежать запуска миграций из каждой replica?

## Что отвечать на собеседовании?

Я бы объяснял Docker-проект через архитектуру services. Сначала называю контейнеры и их роли, затем объясняю Dockerfile и Compose: какие images собираются, какие official images используются, как работает сеть и service DNS, где volumes, какие ports опубликованы, как передаются env/secrets и как запускаются migrations. В конце упоминаю production best practices: small image, non-root user, healthcheck, logs и безопасные secrets.

## Частые ошибки

- Начинать с YAML-деталей без общей картины.
- Не уметь объяснить связь services.
- Забывать про volumes.
- Не знать, как проект запускается с нуля.
- Не различать dev и production.
- Не знать, как debug контейнер.

## Мини-шпаргалка

- Начни с services.
- Объясни image build.
- Объясни network/DNS.
- Объясни volumes.
- Объясни env/secrets.
- Объясни migrations.
- Заверши debug и production practices.
