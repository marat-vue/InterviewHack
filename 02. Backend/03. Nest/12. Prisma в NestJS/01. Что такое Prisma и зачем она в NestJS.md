# Что такое Prisma и зачем она в NestJS?

> [!NOTE]
> Prisma - TypeScript ORM для работы с базой данных через типизированный клиент. В NestJS Prisma обычно используют как database layer: controller вызывает service, service вызывает repository или `PrismaService`, а Prisma выполняет запросы к БД.

## Где Prisma находится в архитектуре?

```txt
HTTP request
  -> Controller
    -> Service
      -> Repository или PrismaService
        -> Prisma Client
          -> Database
```

NestJS не заставляет использовать конкретную ORM. Prisma - один из популярных вариантов, потому что хорошо дружит с TypeScript.

## Что дает Prisma?

- описание моделей в `schema.prisma`;
- генерацию типизированного клиента;
- CRUD-методы;
- relation queries;
- nested writes;
- migrations;
- transactions;
- удобный DX для TypeScript.

## Пример запроса

```ts
const users = await this.prisma.user.findMany({
  where: {
    emailVerified: true,
  },
  include: {
    posts: true,
  },
});
```

## Prisma не заменяет SQL-мышление

Prisma скрывает часть SQL, но не отменяет понимание:

- индексов;
- связей таблиц;
- транзакций;
- N+1;
- сложных фильтров;
- стоимости больших `include`.

## Мини-шпаргалка

- Prisma - ORM и typed query client.
- В NestJS Prisma обычно оформляют как provider.
- Модели описываются в `prisma/schema.prisma`.
- После изменения схемы нужно генерировать Prisma Client.
- Для сложных проектов полезен repository layer поверх Prisma.
