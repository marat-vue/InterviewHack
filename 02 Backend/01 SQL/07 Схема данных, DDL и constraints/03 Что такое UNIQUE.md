# Что такое UNIQUE?

> [!NOTE]
> `UNIQUE` гарантирует уникальность значения или комбинации значений в таблице. Его используют для email, username, external id и составных бизнес-ключей.

## Уникальный email

```sql
CREATE TABLE users (
  id bigint PRIMARY KEY,
  email text NOT NULL UNIQUE
);
```

Теперь две строки с одинаковым email сохранить нельзя.

## Составная уникальность

```sql
CREATE TABLE memberships (
  user_id bigint NOT NULL,
  organization_id bigint NOT NULL,
  role text NOT NULL,
  UNIQUE (user_id, organization_id)
);
```

Пользователь может быть в разных организациях, но не должен повторяться в одной организации.

## UNIQUE и NULL

Поведение с `NULL` зависит от СУБД. Во многих базах несколько `NULL` в UNIQUE-колонке допустимы, потому что `NULL` считается неизвестным значением.

## Мини-шпаргалка

- `UNIQUE` защищает от дублей.
- Может быть на одной колонке или наборе колонок.
- Часто создает индекс.
- С `NULL` есть диалектные нюансы.
- Для business uniqueness лучше constraint, а не только проверка в коде.
