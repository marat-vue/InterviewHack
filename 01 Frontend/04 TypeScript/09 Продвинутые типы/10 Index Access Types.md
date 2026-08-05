# Index Access Types

> [!NOTE]
> Indexed access types позволяют достать тип свойства по ключу: `T[K]`. Это type-level аналог обращения `object[key]`.

## Вопрос

Что такое `Index Access Types`?

## Базовый пример

```typescript
type User = {
  id: number;
  name: string;
  email: string;
};

type UserName = User["name"];
// string
```

Ключ указывается в квадратных скобках на уровне типов.

## Несколько ключей

```typescript
type UserPublicValue = User["id" | "name"];
// number | string
```

Если ключей несколько, результатом будет union типов значений.

## С `keyof`

```typescript
type UserValue = User[keyof User];
// number | string
```

Так можно получить union всех типов значений объекта.

## В generic-функции

```typescript
function getProperty<T, K extends keyof T>(object: T, key: K): T[K] {
  return object[key];
}
```

`T[K]` делает результат точным: для ключа `"name"` вернется `string`, для `"id"` - `number`.

## С массивами

```typescript
type Users = User[];
type UserItem = Users[number];
// User
```

`ArrayType[number]` достает тип элемента массива.

## Мини-шпаргалка

- `T[K]` достает тип значения по ключу.
- `T["a" | "b"]` возвращает union значений.
- `T[keyof T]` - union всех значений объекта.
- `Array[number]` достает тип элемента массива.
