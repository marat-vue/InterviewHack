# Оператор keyof

> [!NOTE] Коротко
> `keyof` получает union ключей объектного типа. Например, `keyof User` превращается в `"id" | "name" | "email"`.

## Вопрос

Что делает оператор `keyof`?

## Базовый пример

```typescript
type User = {
  id: number;
  name: string;
  email: string;
};

type UserKey = keyof User;
// "id" | "name" | "email"
```

## Безопасный доступ к полю

```typescript
function getValue<T, K extends keyof T>(object: T, key: K): T[K] {
  return object[key];
}

const user = { id: 1, name: "Анна" };

const name = getValue(user, "name");
// string
```

`keyof` не дает передать несуществующий ключ.

## В mapped types

```typescript
type Optional<T> = {
  [K in keyof T]?: T[K];
};
```

Так работает множество utility-типов.

## С index signature

```typescript
type Dictionary = {
  [key: string]: number;
};

type DictionaryKey = keyof Dictionary;
// string | number
```

Числа попадают в ключи из-за правил JavaScript: числовые ключи приводятся к строкам.

## Мини-шпаргалка

- `keyof T` возвращает union ключей `T`.
- Часто используется с `K extends keyof T`.
- В mapped types перебирает поля объекта.
- Вместе с `T[K]` дает точную типизацию доступа к свойствам.
