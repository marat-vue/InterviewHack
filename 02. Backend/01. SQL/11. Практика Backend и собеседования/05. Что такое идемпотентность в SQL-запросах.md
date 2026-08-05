# Что такое идемпотентность в SQL-запросах?

> [!NOTE]
> Идемпотентность означает, что повторное выполнение операции дает тот же итоговый результат, что и первое. В backend это важно для retries, платежей, очередей и сетевых сбоев.

## Простой пример

```sql
UPDATE orders
SET status = 'cancelled'
WHERE id = 1;
```

Повторное выполнение оставит статус `cancelled`.

## Неидемпотентный пример

```sql
UPDATE accounts
SET balance = balance - 100
WHERE id = 1;
```

Повторный запуск снова спишет деньги.

## Idempotency key

```sql
CREATE TABLE payment_requests (
  idempotency_key text PRIMARY KEY,
  payment_id bigint NOT NULL
);
```

При повторном запросе приложение проверяет ключ и не создает платеж второй раз.

## UPSERT

```sql
INSERT INTO payment_requests (idempotency_key, payment_id)
VALUES ('req-123', 10)
ON CONFLICT (idempotency_key) DO NOTHING;
```

## Мини-шпаргалка

- Идемпотентная операция безопасна при повторе.
- Retries без идемпотентности могут дублировать эффекты.
- Для платежей нужен idempotency key.
- `UPSERT` помогает строить идемпотентные операции.
- Важно думать не только о SQL, но и о бизнес-эффекте.
