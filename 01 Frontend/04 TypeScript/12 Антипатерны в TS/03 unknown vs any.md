# unknown vs any

> [!NOTE]
> `unknown` означает "тип неизвестен, сначала проверь". `any` означает "не проверяй". Поэтому `unknown` безопаснее для внешних данных и границ системы.

## Вопрос

Чем `unknown` отличается от `any`?

## `any` отключает проверку

```typescript
const value: any = "hello";

value.toFixed(2); // TypeScript разрешает
```

Если значение не число, ошибка появится только во время выполнения.

## `unknown` требует проверку

```typescript
const value: unknown = "hello";

// value.toUpperCase(); // ошибка

if (typeof value === "string") {
  value.toUpperCase(); // теперь можно
}
```

`unknown` сохраняет безопасность: пока тип не сужен, с ним нельзя обращаться как с конкретным значением.

## Данные из API

```typescript
async function loadJSON(url: string): Promise<unknown> {
  const response = await fetch(url);
  return response.json();
}
```

Дальше данные нужно проверить через guard, схему валидации или ручные проверки.

## Когда что выбирать

`unknown` выбирают для входа из внешнего мира: API, `JSON.parse`, `localStorage`, `postMessage`, параметры URL. `any` оставляют для редких технических мест, где невозможно выразить тип безопасно.

## Мини-шпаргалка

- `any` = TypeScript не проверяет.
- `unknown` = TypeScript требует narrowing.
- `unknown` безопасен на границах приложения.
- После guard `unknown` становится конкретным типом.
