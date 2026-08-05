# Какие инструкции Dockerfile нужно знать?

> [!NOTE]
> В Dockerfile чаще всего используют `FROM`, `WORKDIR`, `COPY`, `RUN`, `CMD`, `ENTRYPOINT`, `EXPOSE`, `ENV`, `ARG`, `USER`, `LABEL` и иногда `HEALTHCHECK`. Для собеседования важно понимать, когда выполняется каждая инструкция и что попадает в image.

## FROM

Задает base image:

```dockerfile
FROM node:22-alpine
```

Dockerfile почти всегда начинается с `FROM`. В multi-stage build может быть несколько `FROM`.

## WORKDIR

Задает рабочую директорию:

```dockerfile
WORKDIR /app
```

После этого `COPY`, `RUN`, `CMD` будут работать относительно `/app`.

## COPY

Копирует файлы из build context в image:

```dockerfile
COPY package*.json ./
COPY src ./src
```

Для обычных проектов чаще используют `COPY`, а не `ADD`.

## RUN

Выполняется во время сборки image:

```dockerfile
RUN npm ci
RUN npm run build
```

Результат команды сохраняется в layer.

## CMD

Default command при запуске container:

```dockerfile
CMD ["node", "dist/main.js"]
```

`CMD` можно переопределить в `docker run`.

## ENTRYPOINT

Фиксирует executable контейнера:

```dockerfile
ENTRYPOINT ["node"]
CMD ["dist/main.js"]
```

Часто используется для CLI-images.

## EXPOSE

Документирует порт, который слушает приложение:

```dockerfile
EXPOSE 3000
```

Важно: `EXPOSE` сам не публикует порт на host. Для доступа с host нужен `-p` или `ports` в Compose.

## ENV

Задает переменную окружения внутри image/container:

```dockerfile
ENV NODE_ENV=production
```

Не используй `ENV` для секретов.

## ARG

Build-time переменная:

```dockerfile
ARG NODE_VERSION=22
FROM node:${NODE_VERSION}-alpine
```

`ARG` доступен во время сборки. Это не безопасное место для secrets, потому что значения могут попасть в историю build.

## USER

Переключает пользователя:

```dockerfile
USER node
```

В production лучше не запускать приложение под root без необходимости.

## HEALTHCHECK

Описывает проверку здоровья container:

```dockerfile
HEALTHCHECK --interval=30s --timeout=3s \
  CMD wget -qO- http://localhost:3000/health || exit 1
```

В Compose healthcheck часто задают прямо в `compose.yaml`.

## Что отвечать на собеседовании?

Ключевые инструкции Dockerfile: `FROM` выбирает base image, `WORKDIR` задает директорию, `COPY` переносит файлы, `RUN` выполняет команды при сборке, `CMD` задает команду запуска, `ENTRYPOINT` задает основной executable, `EXPOSE` документирует порт, `ENV` задает runtime env, `ARG` - build-time переменные, `USER` снижает привилегии.

## Частые ошибки

- Путать `RUN` и `CMD`.
- Думать, что `EXPOSE` пробрасывает порт.
- Использовать `ARG` или `ENV` для secrets.
- Не задавать `WORKDIR`.
- Запускать production app под root.
- Использовать shell form там, где лучше exec form.

## Мини-шпаргалка

- `FROM` - base image.
- `WORKDIR` - рабочая папка.
- `COPY` - файлы в image.
- `RUN` - build time.
- `CMD` - runtime default command.
- `ENTRYPOINT` - runtime executable.
- `EXPOSE` - документация порта.
- `USER` - пользователь процесса.
