# Как работают ORDER BY, LIMIT и OFFSET?

> [!NOTE]
> `ORDER BY` задает порядок строк, `LIMIT` ограничивает количество строк, а `OFFSET` пропускает первые N строк. Вместе они часто используются для сортировки и пагинации.

## Сортировка

```sql
SELECT id, title, created_at
FROM posts
ORDER BY created_at DESC;
```

`DESC` сортирует по убыванию, `ASC` - по возрастанию.

## Несколько полей

```sql
SELECT *
FROM products
ORDER BY category_id ASC, price DESC;
```

Сначала сортировка по категории, внутри категории - по цене.

## LIMIT

```sql
SELECT *
FROM posts
ORDER BY created_at DESC
LIMIT 10;
```

Вернет 10 последних записей.

## OFFSET

```sql
SELECT *
FROM posts
ORDER BY created_at DESC
LIMIT 10 OFFSET 20;
```

Пропустит первые 20 строк и вернет следующие 10.

## Важный нюанс

Пагинация через большой `OFFSET` может быть медленной: базе все равно приходится найти и пропустить много строк. Для больших списков часто лучше cursor pagination.

## Мини-шпаргалка

- Без `ORDER BY` порядок строк не гарантирован.
- `LIMIT` ограничивает результат.
- `OFFSET` пропускает строки.
- Большой `OFFSET` может быть дорогим.
- Для стабильной пагинации сортируй по уникальному набору полей.
