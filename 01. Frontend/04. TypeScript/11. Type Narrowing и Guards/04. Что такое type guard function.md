# Что такое type guard function?

> [!NOTE]
> Type guard function - это функция-проверка с возвращаемым типом `value is Type`. Если она вернула `true`, TypeScript сужает значение до `Type`.

## Вопрос

Что такое `type guard function`?

## Базовый пример

```typescript
type User = {
  id: number;
  name: string;
};

function isUser(value: unknown): value is User {
  return (
    typeof value === "object" &&
    value !== null &&
    "id" in value &&
    "name" in value
  );
}
```

`value is User` - type predicate.

## Использование

```typescript
function render(value: unknown) {
  if (isUser(value)) {
    console.log(value.name);
  }
}
```

Внутри `if` TypeScript считает `value` типом `User`.

## Guard для union

```typescript
type Admin = User & { role: "admin"; permissions: string[] };
type Person = User | Admin;

function isAdmin(person: Person): person is Admin {
  return "permissions" in person;
}
```

## Важное правило

TypeScript доверяет guard-функции. Если проверка написана неверно, типы будут выглядеть безопасно, но runtime может упасть.

## Мини-шпаргалка

- Форма: `function isX(value: unknown): value is X`.
- Возвращает boolean на runtime.
- Сужает тип при `true`.
- Хорошо подходит для API-данных и сложных union.
