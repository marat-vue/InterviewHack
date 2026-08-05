# Как подключить Better Auth к Prisma?

> [!NOTE]
> Better Auth подключается к Prisma через `@better-auth/prisma-adapter`. Adapter получает `PrismaClient` и provider базы, например `postgresql`, `mysql` или `sqlite`.

## Установка adapter

```bash
npm install @better-auth/prisma-adapter
```

## auth.ts с Prisma adapter

```ts
import { betterAuth } from 'better-auth';
import { prismaAdapter } from 'better-auth/adapters/prisma';
import { PrismaClient } from '@prisma/client';

const prisma = new PrismaClient();

export const auth = betterAuth({
  database: prismaAdapter(prisma, {
    provider: 'postgresql',
  }),
  emailAndPassword: {
    enabled: true,
  },
});
```

Если в Prisma настроен custom output path, Prisma Client нужно импортировать из generated path.

## Auth schema

Better Auth нужны таблицы для users, sessions, accounts и других сущностей. Для Prisma adapter CLI генерирует Prisma schema, но миграции применяются через Prisma.

```bash
npx auth@latest generate
npx prisma migrate dev --name add_better_auth
```

## Joins

Better Auth Prisma adapter поддерживает experimental joins.

```ts
export const auth = betterAuth({
  experimental: {
    joins: true,
  },
});
```

Для joins в Prisma schema должны быть описаны relations.

## Мини-шпаргалка

- Better Auth Prisma adapter: `@better-auth/prisma-adapter`.
- Adapter получает `PrismaClient`.
- Provider должен соответствовать базе.
- CLI `auth generate` генерирует schema.
- Миграции для Prisma применяются через Prisma tools.
