# Что такое partial и expression index?

> [!NOTE]
> Partial index индексирует только часть строк, а expression index строится по выражению. Они помогают ускорять частые специфичные запросы без индексации всей таблицы.

## Partial index

```sql
CREATE INDEX idx_orders_unpaid
ON orders(created_at)
WHERE status = 'unpaid';
```

Полезно, если неоплаченных заказов мало, но их часто ищут.

```sql
SELECT *
FROM orders
WHERE status = 'unpaid'
ORDER BY created_at;
```

## Expression index

```sql
CREATE INDEX idx_users_lower_email
ON users (lower(email));
```

Запрос:

```sql
SELECT *
FROM users
WHERE lower(email) = lower('Anna@Example.com');
```

## Когда использовать?

- редкие статусы;
- soft delete;
- поиск без учета регистра;
- вычисляемые ключи;
- JSON-поля в PostgreSQL.

## Мини-шпаргалка

- Partial index индексирует часть таблицы.
- Expression index индексирует результат выражения.
- Условие запроса должно совпадать с идеей индекса.
- Такие индексы экономят место.
- Поддержка и синтаксис зависят от СУБД.
