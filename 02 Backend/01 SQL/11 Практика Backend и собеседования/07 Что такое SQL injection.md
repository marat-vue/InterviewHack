# Что такое SQL injection?

> [!NOTE]
> SQL injection - уязвимость, при которой пользовательский ввод попадает в SQL-строку как код. Защита - параметризованные запросы, prepared statements, валидация input и отказ от ручной склейки SQL.

## Опасный код

```js
const sql = `SELECT * FROM users WHERE email = '${email}'`;
```

Если `email` содержит SQL-фрагмент, запрос может изменить смысл.

## Безопасный подход

```js
const result = await db.query(
  'SELECT * FROM users WHERE email = $1',
  [email],
);
```

Параметр передается отдельно от текста SQL, поэтому база воспринимает его как значение, а не как код.

## Где еще риск?

- `ORDER BY` из пользовательского ввода;
- динамические имена таблиц;
- raw SQL в ORM;
- фильтры админки;
- импорт CSV;
- search forms.

## Валидация allowlist

Для направлений сортировки и имен колонок лучше использовать allowlist.

```js
const allowedSort = {
  createdAt: 'created_at',
  email: 'email',
};
```

## Мини-шпаргалка

- Не склеивай SQL с пользовательским вводом.
- Используй параметры.
- Для имен колонок нужны allowlist-ы.
- ORM не спасает, если писать raw SQL небезопасно.
- SQL injection - критичная backend-уязвимость.
