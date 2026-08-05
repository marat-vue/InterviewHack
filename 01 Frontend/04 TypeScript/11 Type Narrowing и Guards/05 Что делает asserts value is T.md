# Что делает asserts value is T?

> [!NOTE]
> `asserts value is T` описывает функцию-утверждение: если функция завершилась без ошибки, TypeScript считает, что `value` имеет тип `T`.

## Вопрос

Что делает `asserts value is T`?

## Отличие от type guard

Type guard возвращает `true` или `false`.

```typescript
function isString(value: unknown): value is string {
  return typeof value === "string";
}
```

Assertion-функция либо ничего не возвращает, либо бросает ошибку.

```typescript
function assertString(value: unknown): asserts value is string {
  if (typeof value !== "string") {
    throw new Error("Expected string");
  }
}
```

## Использование

```typescript
function printUpper(value: unknown) {
  assertString(value);

  console.log(value.toUpperCase());
}
```

После `assertString(value)` TypeScript считает `value` строкой.

## Assertion для объекта

```typescript
function assertUser(value: unknown): asserts value is User {
  if (
    typeof value !== "object" ||
    value === null ||
    !("id" in value) ||
    !("name" in value)
  ) {
    throw new Error("Expected User");
  }
}
```

## Когда использовать

Assertion-функции удобны для валидации входных данных, инвариантов и кода, где дальнейшее выполнение не имеет смысла без правильного типа.

## Мини-шпаргалка

- `asserts value is T` сужает тип после успешного выполнения.
- При ошибке функция обычно бросает `throw`.
- Не возвращает boolean для `if`.
- TypeScript доверяет такой функции, поэтому проверка должна быть честной.
