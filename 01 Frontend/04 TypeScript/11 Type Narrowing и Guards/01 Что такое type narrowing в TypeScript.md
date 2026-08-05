# Что такое type narrowing в TypeScript?

> [!NOTE]
> Type narrowing - это процесс, при котором TypeScript сужает широкий тип до более конкретного после проверки в коде.

## Вопрос

Что такое `type narrowing` в TypeScript?

## Базовый пример

```typescript
function format(value: string | number): string {
  if (typeof value === "string") {
    return value.toUpperCase();
  }

  return value.toFixed(2);
}
```

Сначала `value` имеет тип `string | number`. После проверки `typeof` в первой ветке это `string`, во второй - `number`.

## Зачем это нужно

TypeScript не позволяет использовать свойства, которые есть не у всех вариантов union.

```typescript
function print(value: string | number) {
  // value.toUpperCase(); // ошибка
}
```

Narrowing делает код безопасным и понятным для компилятора.

## Основные способы

```typescript
typeof value === "string";
value instanceof Date;
"data" in result;
state.status === "success";
```

## С `unknown`

```typescript
function parse(value: unknown): string {
  if (typeof value === "string") {
    return value.trim();
  }

  return "";
}
```

## Мини-шпаргалка

- Narrowing уточняет тип после проверки.
- Работает с `if`, `switch`, `return`, `throw`.
- Особенно полезен для union и `unknown`.
- Чем лучше модель типов, тем проще narrowing.
