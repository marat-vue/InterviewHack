# Как dockerize Node.js приложение?

> [!NOTE]
> Чтобы dockerize Node.js приложение, нужно выбрать base image Node, правильно установить зависимости, скопировать код, собрать проект, оставить в production image только runtime-зависимости и запустить приложение не под root.

## Простой Dockerfile

```dockerfile
FROM node:22-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .

EXPOSE 3000
CMD ["npm", "start"]
```

Подходит для первого знакомства, но для production лучше multi-stage.

## Production Dockerfile для TypeScript API

```dockerfile
FROM node:22-alpine AS deps
WORKDIR /app
COPY package*.json ./
RUN npm ci

FROM node:22-alpine AS build
WORKDIR /app
COPY --from=deps /app/node_modules ./node_modules
COPY . .
RUN npm run build

FROM node:22-alpine AS runner
WORKDIR /app
ENV NODE_ENV=production
COPY package*.json ./
RUN npm ci --omit=dev
COPY --from=build /app/dist ./dist
USER node
EXPOSE 3000
CMD ["node", "dist/main.js"]
```

## .dockerignore

```dockerignore
node_modules
dist
coverage
.git
.env
.env.*
*.log
Dockerfile*
compose*.yaml
```

Это ускоряет build и защищает от случайного попадания secrets.

## Compose для dev

```yaml
services:
  api:
    build:
      context: .
      target: deps
    command: npm run dev
    ports:
      - "3000:3000"
    volumes:
      - .:/app
      - /app/node_modules
    env_file:
      - .env
```

В dev можно использовать bind mount для hot reload.

## На что обратить внимание?

- Приложение внутри container должно слушать `0.0.0.0`, а не только `localhost`.
- Порт в `EXPOSE` должен совпадать с портом приложения.
- `NODE_ENV=production` влияет на зависимости и поведение фреймворков.
- Не копируй `.env` в image.
- Не запускай production под root без необходимости.

## Что отвечать на собеседовании?

Для Node.js проекта Dockerfile обычно копирует package files, запускает `npm ci`, копирует исходники, делает build и запускает `node dist/main.js`. Для production лучше multi-stage build: отдельно dependencies/build stage и маленький runtime stage с production dependencies. Важно использовать `.dockerignore`, не класть secrets в image и запускать процесс под non-root user.

## Частые ошибки

- Делать `COPY . .` перед `npm ci`.
- Использовать `npm install` вместо `npm ci` в воспроизводимой сборке.
- Класть `.env` в image.
- Забывать `0.0.0.0` для dev server/API.
- Оставлять devDependencies в production image.
- Не учитывать native dependencies для Alpine.

## Мини-шпаргалка

- Node image: `node:22-alpine` или Debian-based.
- Сначала lock-файлы, потом `npm ci`.
- Потом source code.
- TypeScript build -> `dist`.
- Production stage -> только runtime.
- `USER node` лучше root.
