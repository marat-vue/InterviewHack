# Чем отличаются INNER JOIN и LEFT JOIN?

> [!NOTE]
> `INNER JOIN` возвращает только совпавшие строки из обеих таблиц. `LEFT JOIN` возвращает все строки из левой таблицы и добавляет данные справа, если совпадение найдено; иначе справа будут `NULL`.

## INNER JOIN

```sql
SELECT u.email, o.id AS order_id
FROM users u
INNER JOIN orders o ON o.user_id = u.id;
```

Вернутся только пользователи, у которых есть заказы.

## LEFT JOIN

```sql
SELECT u.email, o.id AS order_id
FROM users u
LEFT JOIN orders o ON o.user_id = u.id;
```

Вернутся все пользователи. У пользователей без заказов `order_id` будет `NULL`.

## Частый вопрос

Найти пользователей без заказов:

```sql
SELECT u.*
FROM users u
LEFT JOIN orders o ON o.user_id = u.id
WHERE o.id IS NULL;
```

## Ловушка с WHERE

```sql
SELECT u.email, o.id
FROM users u
LEFT JOIN orders o ON o.user_id = u.id
WHERE o.status = 'paid';
```

Такой `WHERE` фактически превращает `LEFT JOIN` в `INNER JOIN`, потому что строки без заказа имеют `o.status = NULL`.

## Мини-шпаргалка

- `INNER JOIN` - только совпадения.
- `LEFT JOIN` - все строки слева.
- Справа при отсутствии совпадения будут `NULL`.
- Фильтры по правой таблице в `WHERE` могут сломать смысл `LEFT JOIN`.
- Для "без связанных строк" часто используют `LEFT JOIN ... WHERE right.id IS NULL`.
