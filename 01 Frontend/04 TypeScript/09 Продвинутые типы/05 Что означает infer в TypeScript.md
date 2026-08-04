# Что означает infer в TypeScript?

> [!NOTE] Коротко
> `infer` достает часть типа из шаблона внутри conditional type. Это способ сказать TypeScript: "выведи этот вложенный тип сам".

## Вопрос

Что означает `infer` в TypeScript?

## Базовый пример

```typescript
type ArrayItem<T> = T extends Array<infer Item> ? Item : never;

type A = ArrayItem<number[]>;
// number
```

`Item` - временное имя для типа элемента массива.

## Из функции

```typescript
type Return<T> = T extends (...args: any[]) => infer R ? R : never;

type A = Return<() => string>;
// string
```

## Из Promise

```typescript
type AwaitedValue<T> = T extends Promise<infer Value> ? Value : T;

type User = AwaitedValue<Promise<{ id: number }>>;
// { id: number }
```

## Из tuple

```typescript
type First<T> = T extends [infer Head, ...unknown[]] ? Head : never;

type A = First<[string, number, boolean]>;
// string
```

## Мини-шпаргалка

- `infer` работает только в conditional type.
- Он достает тип из совпавшего шаблона.
- Часто используется для массивов, функций, Promise и tuple.
- Встроенные utility-типы активно используют этот прием.
