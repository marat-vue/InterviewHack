# Что такое materialized view?

> [!NOTE]
> Materialized view хранит результат запроса физически, в отличие от обычной view, которая обычно пересчитывается при обращении. Это полезно для тяжелых отчетов, которые можно обновлять периодически.

## Обычная view

```sql
CREATE VIEW user_stats AS
SELECT user_id, COUNT(*) AS orders_count
FROM orders
GROUP BY user_id;
```

Обычно хранится запрос, а не результат.

## Materialized view

```sql
CREATE MATERIALIZED VIEW user_stats_mv AS
SELECT user_id, COUNT(*) AS orders_count
FROM orders
GROUP BY user_id;
```

Результат хранится как данные.

## Обновление

```sql
REFRESH MATERIALIZED VIEW user_stats_mv;
```

Материализованное представление может устаревать, поэтому нужна стратегия обновления.

## Мини-шпаргалка

- View хранит запрос.
- Materialized view хранит результат.
- Подходит для тяжелых отчетов.
- Требует обновления.
- Может иметь индексы, если СУБД поддерживает.
