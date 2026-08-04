# Как описывать связи в Prisma?

> [!NOTE]
> Связи в Prisma описывают через relation fields и scalar foreign key fields. Самые частые варианты: one-to-many, one-to-one и many-to-many.

## One-to-many

Один пользователь может иметь много постов.

```prisma
model User {
  id    Int    @id @default(autoincrement())
  email String @unique
  posts Post[]
}

model Post {
  id       Int  @id @default(autoincrement())
  title    String
  authorId Int
  author   User @relation(fields: [authorId], references: [id])
}
```

`authorId` - foreign key, `author` - relation field.

## One-to-one

```prisma
model User {
  id      Int      @id @default(autoincrement())
  profile Profile?
}

model Profile {
  id     Int  @id @default(autoincrement())
  userId Int  @unique
  user   User @relation(fields: [userId], references: [id])
}
```

`userId` уникален, потому что один user имеет один profile.

## Many-to-many

```prisma
model Post {
  id   Int   @id @default(autoincrement())
  tags Tag[]
}

model Tag {
  id    Int    @id @default(autoincrement())
  posts Post[]
}
```

Prisma может создать implicit many-to-many relation.

## Мини-шпаргалка

- Relation field связывает модели на уровне Prisma.
- Scalar FK field хранит внешний ключ.
- `@relation(fields: [...], references: [...])` задает связь.
- One-to-one часто требует `@unique` на FK.
- Для сложной many-to-many иногда лучше явная join model.
