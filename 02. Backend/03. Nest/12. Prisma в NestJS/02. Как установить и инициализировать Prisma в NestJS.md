# Как установить и инициализировать Prisma в NestJS?

> [!NOTE]
> Для подключения Prisma устанавливают CLI `prisma` как dev dependency, Prisma Client как runtime dependency, затем запускают `prisma init`, настраивают `DATABASE_URL`, описывают модели и генерируют клиент.

## Установка

```bash
npm install @prisma/client
npm install -D prisma
```

## Инициализация

```bash
npx prisma init
```

Обычно команда создает:

```txt
prisma/
  schema.prisma
.env
```

## DATABASE_URL

```env
DATABASE_URL="postgresql://user:password@localhost:5432/app?schema=public"
```

Для SQLite в учебном проекте:

```env
DATABASE_URL="file:./dev.db"
```

## Генерация клиента

```bash
npx prisma generate
```

После изменения `schema.prisma` клиент нужно сгенерировать заново.

## Мини-шпаргалка

- `prisma` - CLI для схемы и миграций.
- `@prisma/client` - runtime клиент в приложении.
- `prisma init` создает `schema.prisma`.
- `DATABASE_URL` лежит в env.
- `prisma generate` обновляет типизированный клиент.
