# Как работать с env variables в Vite?

> [!NOTE]
> Vite загружает env variables из `.env` файлов, но в client bundle попадают только переменные с префиксом `VITE_`. Все, что доступно frontend-коду, нельзя считать секретом.

## .env

```env
VITE_API_URL=https://api.example.com
VITE_APP_NAME=Frontend App
```

Использование:

```typescript
const apiUrl = import.meta.env.VITE_API_URL;
```

## Почему нужен префикс VITE_?

Vite специально открывает client-side коду только переменные с разрешенным префиксом.

Плохо:

```env
DATABASE_URL=postgres://...
JWT_SECRET=secret
```

Эти значения вообще не должны быть нужны frontend-приложению. Если переменная попадает в browser bundle, пользователь может ее увидеть.

## Mode files

```txt
.env
.env.local
.env.development
.env.production
```

Для production build:

```bash
npm run build
```

Vite загрузит production mode переменные.

Можно указать mode:

```bash
vite build --mode staging
```

и использовать:

```txt
.env.staging
```

## TypeScript typing

```typescript
/// <reference types="vite/client" />
```

Для строгой типизации можно описать env:

```typescript
interface ImportMetaEnv {
  readonly VITE_API_URL: string;
}
```

## Мини-шпаргалка

- Client env должны начинаться с `VITE_`.
- Читай env через `import.meta.env`.
- Frontend env не являются секретами.
- `.env.production` используется для production mode.
- `--mode staging` позволяет загрузить `.env.staging`.
