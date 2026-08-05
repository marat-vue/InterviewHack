# Что такое discriminated union?

> [!NOTE]
> Discriminated union - это union объектов с общим полем-дискриминатором. По значению этого поля TypeScript точно определяет конкретный вариант объекта.

## Вопрос

Что такое `discriminated union`?

## Базовый пример

```typescript
type Loading = { status: "loading" };
type Success = { status: "success"; data: string[] };
type Failure = { status: "failure"; error: string };

type RequestState = Loading | Success | Failure;
```

`status` - дискриминатор. У каждого варианта свое литеральное значение.

## Как TypeScript сужает тип

```typescript
function render(state: RequestState): string {
  switch (state.status) {
    case "loading":
      return "Загрузка";
    case "success":
      return state.data.join(", ");
    case "failure":
      return state.error;
  }
}
```

В ветке `success` TypeScript знает, что есть `data`. В ветке `failure` - что есть `error`.

## Где использовать

```typescript
type ModalState =
  | { type: "closed" }
  | { type: "open"; title: string }
  | { type: "confirm"; title: string; onConfirm: () => void };
```

Так удобно моделировать состояния UI, события, команды и результаты API.

## Требование к дискриминатору

Поле должно иметь literal type, а не просто `string`.

```typescript
type Good = { kind: "user"; name: string };
type Weak = { kind: string; name: string }; // не дает точного narrowing
```

## Мини-шпаргалка

- Нужен общий ключ: `type`, `kind`, `status`.
- Значение ключа должно быть литералом.
- `switch` по дискриминатору дает понятное сужение.
- Добавляй exhaustive check через `never`.
