# Как делать nested writes в Prisma?

> [!NOTE]
> Nested writes позволяют создавать, связывать, отсоединять и обновлять связанные записи внутри одного Prisma-запроса. Prisma выполняет такие операции транзакционно, если они относятся к одному nested write.

## Create с вложенными данными

```ts
const user = await this.prisma.user.create({
  data: {
    email: 'anna@example.com',
    posts: {
      create: [
        { title: 'First post' },
        { title: 'Second post' },
      ],
    },
  },
});
```

## Connect

Связать с уже существующей записью.

```ts
await this.prisma.post.create({
  data: {
    title: 'NestJS + Prisma',
    author: {
      connect: { id: 1 },
    },
  },
});
```

## Disconnect

```ts
await this.prisma.profile.update({
  where: { id: 1 },
  data: {
    user: {
      disconnect: true,
    },
  },
});
```

## Connect or create

```ts
await this.prisma.post.create({
  data: {
    title: 'Prisma relations',
    tags: {
      connectOrCreate: [
        {
          where: { name: 'prisma' },
          create: { name: 'prisma' },
        },
      ],
    },
  },
});
```

## Мини-шпаргалка

- Nested writes работают со связанными данными.
- `create` создает вложенные записи.
- `connect` связывает существующую запись.
- `disconnect` удаляет связь.
- `connectOrCreate` полезен для тегов и справочников.
