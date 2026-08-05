# Что означает union narrowing?

> [!NOTE]
> Union narrowing - это сужение union-типа до конкретного варианта после проверки: `typeof`, `in`, `instanceof`, сравнение литералов или пользовательский type guard.

## Вопрос

Что означает `union narrowing`?

## Пример с примитивами

```typescript
function format(value: string | number): string {
  if (typeof value === "string") {
    return value.toUpperCase();
  }

  return value.toFixed(2);
}
```

После `typeof value === "string"` TypeScript работает с `value` как со строкой.

## Пример с объектами

```typescript
type Success = { status: "success"; data: string[] };
type Failure = { status: "failure"; error: string };

function getMessage(result: Success | Failure): string {
  if (result.status === "success") {
    return result.data.join(", ");
  }

  return result.error;
}
```

## Narrowing через `in`

```typescript
type User = { name: string };
type Admin = { permissions: string[] };

function render(person: User | Admin) {
  if ("permissions" in person) {
    console.log(person.permissions);
  }
}
```

## Почему это важно

Без narrowing TypeScript разрешает только общие для всех вариантов операции. Сужение делает работу с union безопасной.

## Мини-шпаргалка

- Union narrowing уточняет вариант union.
- Для примитивов используй `typeof`.
- Для классов - `instanceof`.
- Для объектов - `in` или дискриминатор.
