# Что выбрать IN или EXISTS?

> [!NOTE]
> `IN` проверяет вхождение значения в список, а `EXISTS` проверяет наличие строк в подзапросе. Для маленьких явных списков удобен `IN`, для проверки связанных строк часто лучше `EXISTS`.

## IN со списком

```sql
SELECT *
FROM orders
WHERE status IN ('paid', 'shipped', 'completed');
```

Это читаемо и удобно.

## IN с подзапросом

```sql
SELECT *
FROM users
WHERE id IN (
  SELECT user_id
  FROM orders
);
```

## EXISTS

```sql
SELECT *
FROM users u
WHERE EXISTS (
  SELECT 1
  FROM orders o
  WHERE o.user_id = u.id
);
```

## NULL-ловушка с NOT IN

```sql
SELECT *
FROM users
WHERE id NOT IN (SELECT user_id FROM orders);
```

Если подзапрос вернет `NULL`, результат может стать неожиданным. `NOT EXISTS` обычно безопаснее.

## Мини-шпаргалка

- `IN` удобен для списков значений.
- `EXISTS` удобен для проверки связанных строк.
- `NOT IN` опасен при `NULL`.
- `NOT EXISTS` часто надежнее для anti join.
- Оптимизатор может преобразовывать варианты, но семантику нужно понимать.
