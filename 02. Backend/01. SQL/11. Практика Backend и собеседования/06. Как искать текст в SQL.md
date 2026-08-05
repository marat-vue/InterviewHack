# Как искать текст в SQL?

> [!NOTE]
> Для простого поиска используют `LIKE` или `ILIKE`, но для больших объемов и релевантности нужен full-text search или внешний поисковый движок. Выбор зависит от размера данных и требований к поиску.

## Простой поиск

```sql
SELECT *
FROM posts
WHERE title ILIKE '%node%';
```

Это удобно, но может быть медленно на больших таблицах.

## Префиксный поиск

```sql
SELECT *
FROM users
WHERE email LIKE 'anna%';
```

Такой поиск чаще может использовать B-tree индекс, чем `'%anna%'`.

## Full-text search

В PostgreSQL есть встроенный full-text search:

```sql
SELECT *
FROM posts
WHERE to_tsvector('english', title || ' ' || body)
      @@ plainto_tsquery('english', 'node streams');
```

## Когда нужен внешний поиск?

Elasticsearch, OpenSearch, Meilisearch или Typesense могут понадобиться, если нужны сложная релевантность, опечатки, морфология, faceted search и большой объем поисковых запросов.

## Мини-шпаргалка

- `LIKE` подходит для простых шаблонов.
- `ILIKE` в PostgreSQL ищет без учета регистра.
- `LIKE '%text%'` часто плохо индексируется.
- Full-text search лучше для документов.
- Внешний поисковый движок нужен не всегда.
