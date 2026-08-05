# Что такое Better Auth и зачем он в NestJS?

> [!NOTE]
> Better Auth - framework-agnostic auth-библиотека для TypeScript-приложений. В NestJS ее можно подключить через community integration `@thallesp/nestjs-better-auth`, чтобы получить готовые auth endpoints, session handling, decorators и guards.

## Что решает Better Auth?

Better Auth берет на себя типовые auth-задачи:

- регистрация;
- вход;
- session management;
- cookies;
- OAuth providers;
- email/password;
- plugins;
- database schema для auth-таблиц.

## Где он живет в NestJS-проекте?

```txt
src/
  auth.ts
  app.module.ts
  users/
  ...
```

`auth.ts` создает Better Auth instance, а `AppModule` подключает `AuthModule.forRoot({ auth })`.

## Важное отличие от ручного JWT

При ручном JWT ты сам пишешь login, refresh, cookies, storage, guards. Better Auth предоставляет готовый auth server и session-based flow, который интегрируется в NestJS.

## Мини-шпаргалка

- Better Auth - готовая auth-система.
- Для NestJS есть community integration.
- Основной файл настройки - `auth.ts`.
- Сессии обычно работают через cookies.
- Для БД можно использовать Prisma adapter.
