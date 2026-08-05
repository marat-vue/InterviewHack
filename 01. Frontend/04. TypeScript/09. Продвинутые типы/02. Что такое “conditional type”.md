# Что такое conditional type?

> [!NOTE]
> Conditional type выбирает один из двух типов по условию: `T extends U ? X : Y`. Это type-level аналог тернарного оператора.

## Вопрос

Что такое `conditional type`?

## Базовый пример

```typescript
type IsString<T> = T extends string ? true : false;

type A = IsString<"hello">;
// true

type B = IsString<number>;
// false
```

Условие проверяет совместимость типов, а не runtime-значения.

## Практический пример

```typescript
type ResponseData<T> = T extends { data: infer Data } ? Data : never;

type UserResponse = { data: { id: number; name: string } };
type User = ResponseData<UserResponse>;
// { id: number; name: string }
```

## Дистрибутивность

Если `T` является union, conditional type распределяется по вариантам.

```typescript
type ToArray<T> = T extends unknown ? T[] : never;

type Result = ToArray<string | number>;
// string[] | number[]
```

Чтобы отключить это поведение, оборачивают тип в tuple.

```typescript
type ToArray<T> = [T] extends [unknown] ? T[] : never;
```

## Мини-шпаргалка

- Форма: `T extends U ? X : Y`.
- Работает на этапе типов.
- Часто используется вместе с `infer`.
- На union обычно распределяется по каждому варианту.
