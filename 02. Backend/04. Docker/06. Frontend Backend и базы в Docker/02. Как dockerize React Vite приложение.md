# Как dockerize React Vite приложение?

> [!NOTE]
> React/Vite приложение в production обычно собирают в статические файлы через Node.js build stage, а затем раздают через Nginx или другой static server. В dev можно запускать Vite dev server внутри контейнера с bind mount.

## Production multi-stage Dockerfile

```dockerfile
FROM node:22-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM nginx:alpine AS runner
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

Здесь:

- Node нужен только для сборки;
- Nginx раздает готовый `dist`;
- final image не содержит source code и devDependencies.

## Dev Compose

```yaml
services:
  frontend:
    image: node:22-alpine
    working_dir: /app
    command: npm run dev -- --host 0.0.0.0
    ports:
      - "5173:5173"
    volumes:
      - .:/app
      - /app/node_modules
```

`--host 0.0.0.0` нужен, чтобы Vite был доступен с host через проброшенный порт.

## Environment variables в Vite

Vite пробрасывает в клиент только переменные с префиксом:

```text
VITE_API_URL=http://localhost:3000
```

В коде:

```ts
const apiUrl = import.meta.env.VITE_API_URL
```

Важно: переменные, попавшие в frontend build, становятся публичными.

## Nginx config для SPA fallback

Для React Router нужен fallback на `index.html`:

```nginx
server {
  listen 80;
  server_name _;

  root /usr/share/nginx/html;
  index index.html;

  location / {
    try_files $uri $uri/ /index.html;
  }
}
```

Dockerfile:

```dockerfile
COPY nginx.conf /etc/nginx/conf.d/default.conf
```

## Что отвечать на собеседовании?

React/Vite production Dockerfile обычно multi-stage: Node stage устанавливает зависимости и выполняет `npm run build`, а final stage на Nginx раздает `/dist`. Для dev используют Node container с bind mount и командой `npm run dev -- --host 0.0.0.0`. Нужно помнить, что Vite env с префиксом `VITE_` попадает в клиентский bundle.

## Частые ошибки

- Запускать Vite dev server как production.
- Забывать `--host 0.0.0.0`.
- Не настраивать SPA fallback в Nginx.
- Класть secrets в `VITE_*`.
- Раздавать source code вместо `dist`.
- Не использовать multi-stage build.

## Мини-шпаргалка

- Build stage: Node.
- Runtime stage: Nginx.
- Vite output: `dist`.
- Dev server: `--host 0.0.0.0`.
- `VITE_*` публично.
- React Router требует fallback.
