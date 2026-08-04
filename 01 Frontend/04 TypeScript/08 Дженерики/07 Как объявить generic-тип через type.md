# Как объявить generic-тип через type?

> [!NOTE] Коротко
> Generic-тип через `type` объявляют с параметром в угловых скобках: `type Box<T> = { value: T }`. Потом этот параметр используют внутри описания типа.

## Вопрос

Как объявить generic-тип через `type`?

## Базовый пример

```typescript
type Box<T> = {
  value: T;
};

type StringBox = Box<string>;
type NumberBox = Box<number>;
```

`Box<T>` - шаблон типа, а `Box<string>` - конкретный тип.

## Generic для ответа API

```typescript
type ApiResponse<T> = {
  data: T;
  error: string | null;
  status: number;
};

type UserResponse = ApiResponse<User>;
type ProductsResponse = ApiResponse<Product[]>;
```

## Несколько параметров

```typescript
type Result<TData, TError> =
  | { ok: true; data: TData }
  | { ok: false; error: TError };
```

## Ограничение generic-типа

```typescript
type EntityMap<T extends { id: string }> = Record<string, T>;
```

Теперь `T` обязан иметь поле `id`.

## Мини-шпаргалка

- `type Name<T> = ...` - generic type alias.
- Подстановка: `Name<string>`, `Name<User[]>`.
- Можно использовать несколько параметров.
- Можно задавать ограничения через `extends`.
