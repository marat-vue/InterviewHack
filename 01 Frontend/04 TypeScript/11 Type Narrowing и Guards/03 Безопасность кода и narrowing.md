# Безопасность кода и narrowing?

> [!NOTE] Коротко
> Narrowing повышает безопасность кода, потому что заставляет проверить значение перед использованием специфичных свойств и методов.

## Вопрос

Как narrowing связан с безопасностью кода?

## Ошибка без проверки

```typescript
function upper(value: string | null): string {
  // return value.toUpperCase(); // ошибка и потенциальный runtime-crash
  return value === null ? "" : value.toUpperCase();
}
```

TypeScript требует обработать `null`, прежде чем вызвать метод строки.

## Данные из внешнего мира

API, `localStorage`, формы и URL-параметры могут вернуть неожиданные данные. Для них полезно начинать с `unknown`.

```typescript
function isUser(value: unknown): value is User {
  return (
    typeof value === "object" &&
    value !== null &&
    "id" in value &&
    "name" in value
  );
}

function handle(value: unknown) {
  if (isUser(value)) {
    console.log(value.name);
  }
}
```

## Безопасные состояния UI

```typescript
type State =
  | { status: "loading" }
  | { status: "success"; data: string[] }
  | { status: "error"; message: string };

function render(state: State) {
  if (state.status === "error") {
    return state.message;
  }
}
```

Невозможно случайно прочитать `message` у состояния `loading`.

## Мини-шпаргалка

- Narrowing убирает небезопасные предположения.
- `unknown` плюс guard безопаснее, чем `any`.
- Discriminated union уменьшает число невозможных состояний.
- Проверки должны соответствовать реальности runtime.
