# discriminant property

> [!NOTE] Коротко
> Discriminant property - это общее поле в union объектов, по которому TypeScript различает варианты. Обычно его называют `type`, `kind`, `status` или `state`.

## Вопрос

Что такое `discriminant property`?

## Базовый пример

```typescript
type UserEvent =
  | { type: "login"; userId: string }
  | { type: "logout"; userId: string }
  | { type: "error"; message: string };
```

Поле `type` - discriminant property.

## Как оно работает

```typescript
function handle(event: UserEvent) {
  if (event.type === "error") {
    console.log(event.message);
    return;
  }

  console.log(event.userId);
}
```

После проверки `event.type === "error"` TypeScript знает точный вариант.

## Хорошие имена

```typescript
type Shape = { kind: "circle"; radius: number } | { kind: "square"; size: number };
type Request = { status: "loading" } | { status: "success"; data: string[] };
type Command = { action: "save" } | { action: "delete"; id: string };
```

Выбирай имя, которое понятно в предметной области.

## Тип значения

Значение дискриминатора должно быть литеральным и уникальным для варианта.

```typescript
type Bad = { type: string; data: string[] };
```

`string` слишком широкий, он не дает точного различения.

## Мини-шпаргалка

- Discriminant property - общий ключ union объектов.
- Значения должны быть литералами.
- Каждый вариант должен иметь свое значение.
- Это основа discriminated union.
