# Что делает Exclude?

> [!NOTE]
> `Exclude<T, U>` удаляет из union `T` все варианты, которые совместимы с `U`.

## Вопрос

Что делает `Exclude`?

## Базовый пример

```typescript
type Status = "idle" | "loading" | "success" | "error";

type FinishedStatus = Exclude<Status, "idle" | "loading">;
// "success" | "error"
```

`Exclude` проходит по каждому варианту union и оставляет только те, которые не подходят под второй тип.

## С примитивами

```typescript
type Value = string | number | boolean;

type WithoutBoolean = Exclude<Value, boolean>;
// string | number
```

## С объектными union

```typescript
type Event =
  | { type: "click"; x: number; y: number }
  | { type: "submit"; formId: string }
  | { type: "reset" };

type NonClickEvent = Exclude<Event, { type: "click" }>;
```

Из union удалится вариант с `type: "click"`.

## Как устроен

Упрощенная версия:

```typescript
type MyExclude<T, U> = T extends U ? never : T;
```

## Мини-шпаргалка

- `Exclude<T, U>` вычитает `U` из union `T`.
- Работает благодаря дистрибутивным conditional types.
- Часто применяется к literal union.
- Противоположная операция - `Extract`.
