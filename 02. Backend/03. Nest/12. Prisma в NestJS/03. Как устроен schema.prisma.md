# Как устроен schema.prisma?

> [!NOTE]
> `schema.prisma` - главный файл Prisma, где описывают datasource, generator и модели данных. Из этой схемы Prisma строит миграции и генерирует Prisma Client.

## Базовая структура

```prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id        Int      @id @default(autoincrement())
  email     String   @unique
  name      String?
  createdAt DateTime @default(now())
}
```

## datasource

`datasource` говорит, к какой базе подключаться.

```prisma
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}
```

## generator

`generator` говорит, какой клиент генерировать.

```prisma
generator client {
  provider = "prisma-client-js"
}
```

В современных версиях Prisma при кастомном output клиент импортируют из указанного generated path, а не обязательно из `@prisma/client`.

## Мини-шпаргалка

- `schema.prisma` описывает БД для Prisma.
- `datasource` задает provider и URL.
- `generator` задает генерацию клиента.
- `model` описывает таблицу/коллекцию.
- После изменения схемы нужны migration/generate.
