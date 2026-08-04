# Что такое union типы?

> [!NOTE] Коротко
> Union type описывает значение, которое может принадлежать одному из нескольких типов. Записывается через `|`.

## Вопрос

Что такое union типы?

## Простое определение

Union - это "выбор из вариантов".

```typescript
type Theme = "light" | "dark";
type Id = string | number;
```

Значение должно подходить хотя бы под один вариант.

```typescript
let theme: Theme = "light";
// theme = "blue"; // ошибка
```

## Почему нельзя сразу использовать все методы

Когда переменная имеет union-тип, TypeScript не знает, какой вариант пришел прямо сейчас.

```typescript
function print(value: string | number) {
  // value.toUpperCase(); // ошибка

  if (typeof value === "string") {
    console.log(value.toUpperCase());
  }
}
```

## Union объектов

```typescript
type Loading = { status: "loading" };
type Success = { status: "success"; data: string[] };
type Failure = { status: "failure"; error: string };

type RequestState = Loading | Success | Failure;
```

Такой тип хорошо моделирует состояния интерфейса.

## Мини-шпаргалка

- Union пишется через `|`.
- Читается как "или".
- Для уникальных свойств нужен narrowing.
- Literal union часто заменяет enum для простых строковых вариантов.
