# Что такое Discriminated Unions?

> [!NOTE] Коротко
> Discriminated Unions - это паттерн для безопасного описания нескольких вариантов объекта через общий ключ-дискриминатор.

## Вопрос

Что такое `Discriminated Unions`?

## Пример с фигурами

```typescript
type Circle = {
  kind: "circle";
  radius: number;
};

type Square = {
  kind: "square";
  size: number;
};

type Shape = Circle | Square;
```

`kind` помогает TypeScript понять, с какой фигурой мы работаем.

## Расчет площади

```typescript
function area(shape: Shape): number {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "square":
      return shape.size ** 2;
  }
}
```

## Состояния запроса

```typescript
type RequestState =
  | { status: "idle" }
  | { status: "loading" }
  | { status: "success"; data: string[] }
  | { status: "error"; message: string };
```

Такой тип не позволяет случайно обратиться к `data`, когда запрос еще загружается.

## Почему лучше, чем набор optional-полей

```typescript
type WeakState = {
  status: string;
  data?: string[];
  message?: string;
};
```

В слабой модели возможно слишком много невалидных комбинаций. Discriminated union оставляет только допустимые состояния.

## Мини-шпаргалка

- Каждый вариант - отдельный объектный тип.
- У всех вариантов есть общий discriminant property.
- Значение дискриминатора - string/number/boolean literal.
- Подходит для состояний, событий и команд.
