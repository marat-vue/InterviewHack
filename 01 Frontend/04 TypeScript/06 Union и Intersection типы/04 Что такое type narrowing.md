# Что такое type narrowing?

> [!NOTE]
> Type narrowing - это сужение типа после проверки. TypeScript анализирует условия и понимает, какой конкретный вариант union сейчас используется.

## Вопрос

Что такое `type narrowing`?

## Простая проверка

```typescript
function format(value: string | number): string {
  if (typeof value === "number") {
    return value.toFixed(2);
  }

  return value.toUpperCase();
}
```

Внутри `if` переменная имеет тип `number`, а после него - `string`.

## Narrowing через `typeof`

Подходит для примитивов.

```typescript
if (typeof value === "string") {
  value.trim();
}
```

## Narrowing через `instanceof`

Подходит для классов и встроенных объектов.

```typescript
function printDate(value: string | Date) {
  if (value instanceof Date) {
    console.log(value.toISOString());
  }
}
```

## Narrowing через `in`

Подходит для объектов с разными полями.

```typescript
type Cat = { meow(): void };
type Dog = { bark(): void };

function speak(pet: Cat | Dog) {
  if ("meow" in pet) {
    pet.meow();
  } else {
    pet.bark();
  }
}
```

## Control flow analysis

TypeScript учитывает `return`, `throw`, `if`, `switch` и другие ветвления.

## Мини-шпаргалка

- Narrowing превращает широкий тип в более конкретный.
- `typeof` - для примитивов.
- `instanceof` - для классов.
- `in` и дискриминаторы - для объектных union.
