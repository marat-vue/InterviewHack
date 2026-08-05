# Что такое RIGHT JOIN и FULL OUTER JOIN?

> [!NOTE]
> `RIGHT JOIN` возвращает все строки из правой таблицы, а `FULL OUTER JOIN` возвращает все строки из обеих таблиц: совпавшие соединяются, несовпавшие получают `NULL` на другой стороне.

## RIGHT JOIN

```sql
SELECT u.email, o.id AS order_id
FROM users u
RIGHT JOIN orders o ON o.user_id = u.id;
```

Вернутся все заказы, даже если для какого-то заказа не найден пользователь.

На практике `RIGHT JOIN` часто переписывают как `LEFT JOIN`, просто поменяв таблицы местами.

```sql
SELECT u.email, o.id AS order_id
FROM orders o
LEFT JOIN users u ON u.id = o.user_id;
```

## FULL OUTER JOIN

```sql
SELECT u.email, o.id AS order_id
FROM users u
FULL OUTER JOIN orders o ON o.user_id = u.id;
```

Вернутся:

- пользователи с заказами;
- пользователи без заказов;
- заказы без найденного пользователя.

## Когда FULL JOIN полезен?

- сверка данных между системами;
- поиск расхождений;
- сравнение таблиц;
- миграции;
- отчеты по missing records.

## Мини-шпаргалка

- `RIGHT JOIN` сохраняет все строки справа.
- `RIGHT JOIN` часто можно заменить на `LEFT JOIN`.
- `FULL OUTER JOIN` сохраняет строки с обеих сторон.
- Несовпавшие значения получают `NULL`.
- Поддержка `FULL OUTER JOIN` есть не во всех СУБД одинаково.
