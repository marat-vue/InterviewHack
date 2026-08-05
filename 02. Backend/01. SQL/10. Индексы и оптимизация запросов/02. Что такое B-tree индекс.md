# Что такое B-tree индекс?

> [!NOTE]
> B-tree - самый распространенный тип индекса в SQL-базах. Он хорошо подходит для поиска по равенству, диапазонам, сортировки и поиска по префиксу.

## Для чего подходит?

```sql
CREATE INDEX idx_orders_created_at
ON orders(created_at);
```

Такой индекс может помочь запросам:

```sql
SELECT *
FROM orders
WHERE created_at >= DATE '2026-01-01';
```

и:

```sql
SELECT *
FROM orders
ORDER BY created_at DESC
LIMIT 20;
```

## Поиск по равенству

```sql
CREATE INDEX idx_users_email
ON users(email);
```

```sql
SELECT *
FROM users
WHERE email = 'a@example.com';
```

## Диапазон

```sql
SELECT *
FROM orders
WHERE total BETWEEN 100 AND 500;
```

B-tree умеет эффективно искать диапазоны.

## Мини-шпаргалка

- B-tree - стандартный индекс по умолчанию во многих СУБД.
- Хорош для `=`, `<`, `>`, `BETWEEN`.
- Может помогать `ORDER BY`.
- Может помогать префиксному `LIKE 'abc%'`.
- Не всегда помогает `LIKE '%abc%'`.
