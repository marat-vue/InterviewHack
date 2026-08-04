# Что такое self join?

> [!NOTE]
> Self join - соединение таблицы самой с собой. Он нужен, когда строки одной таблицы связаны с другими строками этой же таблицы, например сотрудник и менеджер.

## Пример иерархии

```sql
CREATE TABLE employees (
  id bigint PRIMARY KEY,
  name text NOT NULL,
  manager_id bigint REFERENCES employees(id)
);
```

Сотрудник ссылается на своего менеджера в той же таблице.

## Запрос

```sql
SELECT
  e.name AS employee,
  m.name AS manager
FROM employees e
LEFT JOIN employees m ON m.id = e.manager_id;
```

Одна копия таблицы используется как сотрудники, другая - как менеджеры.

## Почему нужны alias?

Без alias база не поймет, к какой роли таблицы относится столбец.

```sql
employees.name -- непонятно: сотрудник или менеджер?
```

## Мини-шпаргалка

- Self join - таблица joined сама с собой.
- Alias обязательны для читаемости.
- Частый пример: employee -> manager.
- Для глубоких деревьев могут понадобиться recursive CTE.
- `LEFT JOIN` нужен, если у корневых строк нет родителя.
