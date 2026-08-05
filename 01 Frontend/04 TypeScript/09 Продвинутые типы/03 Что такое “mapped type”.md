# Что такое mapped type?

> [!NOTE]
> Mapped type создает новый объектный тип, проходя по ключам другого типа. Базовая форма: `{ [K in keyof T]: ... }`.

## Вопрос

Что такое `mapped type`?

## Базовый пример

```typescript
type User = {
  id: number;
  name: string;
};

type Flags<T> = {
  [K in keyof T]: boolean;
};

type UserFlags = Flags<User>;
// { id: boolean; name: boolean }
```

`K` по очереди принимает каждый ключ из `keyof T`.

## Как устроен Partial

```typescript
type MyPartial<T> = {
  [K in keyof T]?: T[K];
};
```

Такой тип делает каждое поле опциональным.

## Как устроен Readonly

```typescript
type MyReadonly<T> = {
  readonly [K in keyof T]: T[K];
};
```

## Переименование ключей

Через `as` можно создавать новые имена ключей.

```typescript
type Getters<T> = {
  [K in keyof T as `get${Capitalize<string & K>}`]: () => T[K];
};
```

## Мини-шпаргалка

- Mapped type перебирает ключи.
- `keyof T` дает union ключей.
- `T[K]` достает тип значения по ключу.
- На mapped types построены `Partial`, `Required`, `Readonly`, `Pick`.
