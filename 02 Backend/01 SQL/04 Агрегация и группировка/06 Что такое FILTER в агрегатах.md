# Что такое FILTER в агрегатах?

> [!NOTE]
> `FILTER` позволяет применять условие к отдельной агрегатной функции. Это удобно, когда нужно посчитать несколько метрик по разным условиям в одном запросе.

## Пример в PostgreSQL

```sql
SELECT
  COUNT(*) AS total_orders,
  COUNT(*) FILTER (WHERE status = 'paid') AS paid_orders,
  COUNT(*) FILTER (WHERE status = 'cancelled') AS cancelled_orders
FROM orders;
```

Один запрос возвращает несколько счетчиков.

## Альтернатива через CASE

Если диалект не поддерживает `FILTER`, можно использовать `CASE`.

```sql
SELECT
  COUNT(*) AS total_orders,
  SUM(CASE WHEN status = 'paid' THEN 1 ELSE 0 END) AS paid_orders
FROM orders;
```

## Когда полезно?

- dashboards;
- аналитика по статусам;
- отчеты;
- условные суммы;
- сравнение активных и неактивных сущностей.

## Мини-шпаргалка

- `FILTER` задает условие для конкретного агрегата.
- Удобен для нескольких метрик в одном запросе.
- В PostgreSQL поддерживается.
- Универсальная альтернатива - `SUM(CASE WHEN ... THEN 1 ELSE 0 END)`.
- `FILTER` читается лучше, чем много вложенных `CASE`.

