# Как описывать модели Prisma?

> [!NOTE]
> Модель Prisma описывает таблицу и ее поля: типы, primary key, default values, unique constraints, optional fields и индексы. По моделям Prisma генерирует типы и методы клиента.

## Пример модели

```prisma
model User {
  id        Int      @id @default(autoincrement())
  email     String   @unique
  name      String?
  role      Role     @default(USER)
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}

enum Role {
  USER
  ADMIN
}
```

## Обязательные и optional поля

```prisma
email String
name  String?
```

`String` обязателен, `String?` может быть `null`.

## Атрибуты

| Атрибут | Значение |
|---|---|
| `@id` | primary key |
| `@default(...)` | значение по умолчанию |
| `@unique` | уникальность |
| `@updatedAt` | автоматически обновлять timestamp |
| `@@index` | индекс на уровне модели |

## Какие типы бывают?

В этой заметке показаны `Int`, `String`, `DateTime` и `enum`, но Prisma поддерживает больше типов: `Boolean`, `BigInt`, `Float`, `Decimal`, `Json`, `Bytes`, nullable fields, scalar lists и native database types через `@db.*`.

Подробный разбор вынесен отдельно: [[14 Какие типы данных поддерживает Prisma]].

## Индексы

```prisma
model Post {
  id        Int      @id @default(autoincrement())
  authorId  Int
  createdAt DateTime @default(now())

  @@index([authorId, createdAt])
}
```

## Мини-шпаргалка

- `model` обычно соответствует таблице.
- `?` делает поле nullable.
- `@unique` нужен для email/slug.
- `@updatedAt` удобен для `updatedAt`.
- Индексы проектируют под реальные запросы.
- Типы данных выбирай под домен: деньги - `Decimal`, даты - `DateTime`, гибкая metadata - `Json`.
