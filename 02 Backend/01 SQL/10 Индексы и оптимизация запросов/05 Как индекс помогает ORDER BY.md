# Как индекс помогает ORDER BY?

> [!NOTE]
> Индекс может помочь `ORDER BY`, если порядок индекса совпадает с нужным порядком запроса. Тогда базе не нужно отдельно сортировать большой набор строк.

## Пример

```sql
CREATE INDEX idx_posts_created_at
ON posts(created_at DESC);
```

Запрос:

```sql
SELECT *
FROM posts
ORDER BY created_at DESC
LIMIT 20;
```

База может пройти по индексу в нужном порядке и быстро взять первые 20 строк.

## Фильтр плюс сортировка

```sql
CREATE INDEX idx_posts_status_created_at
ON posts(status, created_at DESC);
```

```sql
SELECT *
FROM posts
WHERE status = 'published'
ORDER BY created_at DESC
LIMIT 20;
```

Составной индекс помогает сначала найти опубликованные посты, затем взять их в нужном порядке.

## Мини-шпаргалка

- Индекс может убрать отдельную сортировку.
- Особенно полезен с `ORDER BY ... LIMIT`.
- Для фильтра и сортировки часто нужен составной индекс.
- Порядок колонок в индексе важен.
- Проверяй через `EXPLAIN`.
