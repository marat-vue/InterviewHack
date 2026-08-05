# Что такое EXPLAIN?

> [!NOTE]
> `EXPLAIN` показывает план выполнения запроса: как база собирается читать таблицы, использовать индексы, соединять данные, сортировать и агрегировать. Это главный инструмент анализа производительности SQL.

## Пример

```sql
EXPLAIN
SELECT *
FROM users
WHERE email = 'anna@example.com';
```

План показывает, будет ли база делать полный scan таблицы или использовать индекс.

## EXPLAIN ANALYZE

В PostgreSQL:

```sql
EXPLAIN ANALYZE
SELECT *
FROM users
WHERE email = 'anna@example.com';
```

`EXPLAIN` показывает оценку плана, `EXPLAIN ANALYZE` реально выполняет запрос и показывает фактическое время.

## На что смотреть?

- тип scan: sequential scan или index scan;
- estimated rows и actual rows;
- join strategy;
- sort;
- loops;
- total execution time.

## Осторожно

`EXPLAIN ANALYZE` выполняет запрос. Для `UPDATE`, `DELETE`, `INSERT` это может реально изменить данные, если не использовать транзакцию и rollback.

## Мини-шпаргалка

- `EXPLAIN` показывает план.
- `EXPLAIN ANALYZE` выполняет запрос и меряет факт.
- Смотри на scan, rows, sort, join и время.
- План нужно читать вместе со схемой и индексами.
- Анализ планов - навык, а не одна магическая команда.
