# Как собирать строки в список через STRING_AGG?

> [!NOTE]
> Некоторые SQL-диалекты позволяют агрегировать несколько строк в одну строку или массив. В PostgreSQL для строк часто используют `string_agg`, в MySQL - `GROUP_CONCAT`.

## PostgreSQL string_agg

```sql
SELECT
  post_id,
  string_agg(tag_name, ', ' ORDER BY tag_name) AS tags
FROM post_tags
GROUP BY post_id;
```

Результат:

| post_id | tags |
|---|---|
| 1 | `css, html, sql` |

## MySQL GROUP_CONCAT

```sql
SELECT
  post_id,
  GROUP_CONCAT(tag_name ORDER BY tag_name SEPARATOR ', ') AS tags
FROM post_tags
GROUP BY post_id;
```

## Когда полезно?

- собрать теги поста;
- вывести роли пользователя;
- сделать отчет;
- подготовить CSV-подобное поле;
- свернуть one-to-many связь в одну строку результата.

## Осторожно

Если приложению нужен структурированный API, лучше вернуть строки и собрать массив в приложении или использовать JSON aggregation, если СУБД это поддерживает.

## Мини-шпаргалка

- `string_agg` собирает строки в PostgreSQL.
- `GROUP_CONCAT` часто используют в MySQL.
- Порядок внутри агрегации лучше задавать явно.
- У разных СУБД разные лимиты и синтаксис.
- Для API часто удобнее JSON/array aggregation или сборка в приложении.
