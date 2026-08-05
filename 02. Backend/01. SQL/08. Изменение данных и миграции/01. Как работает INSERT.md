# Как работает INSERT?

> [!NOTE]
> `INSERT` добавляет новые строки в таблицу. Он может вставлять одну строку, несколько строк, результат `SELECT`, а в некоторых СУБД возвращать вставленные данные через `RETURNING`.

## Одна строка

```sql
INSERT INTO users (email, name)
VALUES ('anna@example.com', 'Anna');
```

## Несколько строк

```sql
INSERT INTO users (email, name)
VALUES
  ('a@example.com', 'A'),
  ('b@example.com', 'B');
```

## INSERT ... SELECT

```sql
INSERT INTO archived_users (id, email)
SELECT id, email
FROM users
WHERE deleted_at IS NOT NULL;
```

## RETURNING

В PostgreSQL удобно получить созданную строку:

```sql
INSERT INTO users (email)
VALUES ('new@example.com')
RETURNING id, email, created_at;
```

## Мини-шпаргалка

- `INSERT` добавляет строки.
- Явно перечисляй колонки.
- Можно вставлять много строк одним запросом.
- `INSERT ... SELECT` копирует результат запроса.
- `RETURNING` есть не во всех диалектах.
