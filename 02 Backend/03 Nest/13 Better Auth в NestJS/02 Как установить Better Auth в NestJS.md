# Как установить Better Auth в NestJS?

> [!NOTE]
> Для NestJS-проекта устанавливают пакет `better-auth` и Nest integration `@thallesp/nestjs-better-auth`. Если используется Prisma adapter, дополнительно нужен `@better-auth/prisma-adapter`.

## Базовая установка

```bash
npm install better-auth
npm install @thallesp/nestjs-better-auth
```

## Если используется Prisma

```bash
npm install @better-auth/prisma-adapter
```

Также должны быть установлены Prisma-зависимости:

```bash
npm install @prisma/client
npm install -D prisma
```

## Env-переменные

```env
BETTER_AUTH_SECRET="your-long-random-secret-at-least-32-chars"
BETTER_AUTH_URL="http://localhost:3000"
DATABASE_URL="postgresql://user:password@localhost:5432/app"
```

`BETTER_AUTH_SECRET` должен быть длинным, случайным и не должен попадать в Git.

## Где хранить файлы?

Для NestJS удобно:

```txt
src/
  auth.ts
  app.module.ts
```

или:

```txt
src/
  auth/
    auth.ts
```

Главное - чтобы integration module импортировал именно этот `auth` instance.

## Мини-шпаргалка

- `better-auth` - основная библиотека.
- `@thallesp/nestjs-better-auth` - Nest integration.
- `@better-auth/prisma-adapter` нужен для Prisma.
- Нужны `BETTER_AUTH_SECRET` и `BETTER_AUTH_URL`.
- Secret должен быть high entropy и не короче 32 символов.
