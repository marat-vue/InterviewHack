# Как работать со схемой Better Auth через CLI?

> [!NOTE]
> Better Auth CLI умеет генерировать schema под выбранный adapter и plugins. Для Prisma adapter команда `auth generate` обновляет Prisma schema, а миграции затем выполняются инструментами Prisma.

## Generate

```bash
npx auth@latest generate
```

Команда генерирует schema, нужную Better Auth.

## Config path

Если `auth.ts` лежит не в стандартном месте, укажи путь.

```bash
npx auth@latest generate --config src/auth.ts
```

## Output

Для Prisma output по умолчанию связан с `prisma/schema.prisma`.

```bash
npx auth@latest generate --output prisma/schema.prisma
```

## После generate

```bash
npx prisma migrate dev --name add_auth_tables
npx prisma generate
```

Better Auth CLI не применяет Prisma migrations сам за тебя.

## Мини-шпаргалка

- `auth generate` создает schema под config.
- Для Prisma migration делается через Prisma.
- Если config не найден, укажи `--config`.
- Plugins могут добавить свои таблицы.
- Schema changes нужно коммитить и мигрировать.
