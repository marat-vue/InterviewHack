# Чем отличается WHERE от HAVING?

> [!NOTE]
> `WHERE` фильтрует строки до группировки, а `HAVING` фильтрует уже готовые группы после `GROUP BY`. Поэтому условия по агрегатам пишут в `HAVING`.

## WHERE

```sql
SELECT status, COUNT(*)
FROM orders
WHERE created_at >= DATE '2026-01-01'
GROUP BY status;
```

Сначала берутся только заказы за 2026 год, потом они группируются.

## HAVING

```sql
SELECT user_id, COUNT(*) AS orders_count
FROM orders
GROUP BY user_id
HAVING COUNT(*) >= 5;
```

Вернутся пользователи, у которых минимум 5 заказов.

## Частая ошибка

```sql
SELECT user_id, COUNT(*)
FROM orders
WHERE COUNT(*) >= 5
GROUP BY user_id;
```

Так нельзя: `WHERE` выполняется до агрегатов.

## Можно использовать вместе

```sql
SELECT user_id, COUNT(*)
FROM orders
WHERE status = 'paid'
GROUP BY user_id
HAVING COUNT(*) >= 3;
```

Сначала только оплаченные заказы, потом пользователи с минимум тремя такими заказами.

## Мини-шпаргалка

- `WHERE` фильтрует строки.
- `HAVING` фильтрует группы.
- Условия по агрегатам идут в `HAVING`.
- `WHERE` обычно помогает производительности, потому что уменьшает данные до группировки.
- Можно использовать `WHERE` и `HAVING` вместе.
