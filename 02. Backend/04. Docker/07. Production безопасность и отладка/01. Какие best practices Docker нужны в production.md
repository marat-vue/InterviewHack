# Какие best practices Docker нужны в production?

> [!NOTE]
> Production Docker image должен быть воспроизводимым, маленьким, безопасным и предсказуемым. Важно фиксировать версии, использовать multi-stage build, не хранить secrets в image, запускать процесс не под root и логировать в stdout/stderr.

## Фиксируй версии

Плохо:

```dockerfile
FROM node:latest
```

Лучше:

```dockerfile
FROM node:22-alpine
```

Еще строже - использовать digest:

```dockerfile
FROM node:22-alpine@sha256:...
```

## Используй multi-stage build

Production image не должен содержать:

- devDependencies;
- test files;
- build cache;
- source code, если нужен только compiled output;
- package manager cache;
- временные файлы.

## Не запускай под root

```dockerfile
USER node
```

Если процессу не нужны root-права, не давай их.

## Не храни secrets в image

Плохо:

```dockerfile
ENV DATABASE_PASSWORD=super-secret
```

Secrets передают на runtime уровне:

- secret manager;
- orchestrator secrets;
- CI/CD secret variables;
- Docker secrets;
- runtime env.

## Логи в stdout/stderr

Приложение должно писать логи в консоль:

```ts
console.log('server started')
console.error(error)
```

Docker и orchestrator собирают stdout/stderr.

## Один container - один основной процесс

Обычно container запускает один главный процесс:

```dockerfile
CMD ["node", "dist/main.js"]
```

Не нужно без причины запускать внутри одного контейнера backend, database, cron и Nginx одновременно.

## Healthcheck и graceful shutdown

Production app должен:

- иметь `/health` или аналог;
- корректно обрабатывать SIGTERM;
- закрывать HTTP server;
- закрывать DB connections;
- не терять active requests.

## Что отвечать на собеседовании?

Production Docker best practices: фиксировать версии base images, использовать multi-stage build, держать final image маленьким, запускать приложение под non-root user, не хранить secrets в image, писать logs в stdout/stderr, настраивать healthcheck, graceful shutdown и минимизировать поверхность атаки.

## Частые ошибки

- Использовать `latest`.
- Оставлять devDependencies.
- Запускать под root.
- Копировать `.env` в image.
- Писать logs только в файл внутри container.
- Делать один огромный container со всеми сервисами.
- Не обрабатывать SIGTERM.

## Мини-шпаргалка

- Pin versions.
- Multi-stage build.
- Small final image.
- Non-root user.
- No secrets in image.
- Logs -> stdout/stderr.
- Healthcheck + graceful shutdown.
