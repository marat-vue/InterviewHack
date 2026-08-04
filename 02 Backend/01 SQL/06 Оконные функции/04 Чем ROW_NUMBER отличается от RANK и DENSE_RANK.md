# Чем ROW_NUMBER отличается от RANK и DENSE_RANK?

> [!NOTE]
> `ROW_NUMBER` выдает уникальный номер каждой строке, `RANK` дает одинаковый ранг равным значениям с пропусками, а `DENSE_RANK` дает одинаковый ранг без пропусков.

## Пример

```sql
SELECT
  name,
  score,
  ROW_NUMBER() OVER (ORDER BY score DESC) AS row_number,
  RANK() OVER (ORDER BY score DESC) AS rank,
  DENSE_RANK() OVER (ORDER BY score DESC) AS dense_rank
FROM players;
```

Если два игрока делят первое место:

| score | row_number | rank | dense_rank |
|---|---|---|---|
| 100 | 1 | 1 | 1 |
| 100 | 2 | 1 | 1 |
| 90 | 3 | 3 | 2 |

## Когда использовать?

- `ROW_NUMBER` - выбрать одну строку из группы.
- `RANK` - спортивный рейтинг с пропусками.
- `DENSE_RANK` - рейтинг без пропусков.

## Top N per group

```sql
WITH ranked AS (
  SELECT
    *,
    ROW_NUMBER() OVER (
      PARTITION BY user_id
      ORDER BY created_at DESC
    ) AS rn
  FROM orders
)
SELECT *
FROM ranked
WHERE rn = 1;
```

## Мини-шпаргалка

- `ROW_NUMBER` всегда уникален внутри окна.
- `RANK` оставляет пропуски после равных значений.
- `DENSE_RANK` не оставляет пропуски.
- Для "последняя запись в группе" часто нужен `ROW_NUMBER`.
- Для рейтингов выбирай функцию по бизнес-правилу.
