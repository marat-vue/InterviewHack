# Что делает ReturnType?

> [!NOTE]
> `ReturnType<T>` достает тип возвращаемого значения из типа функции `T`.

## Вопрос

Что делает `ReturnType`?

## Базовый пример

```typescript
function createUser(name: string) {
  return {
    id: crypto.randomUUID(),
    name,
  };
}

type User = ReturnType<typeof createUser>;
```

`User` будет типом объекта, который возвращает функция.

## Почему нужен `typeof`

`createUser` - это значение, а `ReturnType` ожидает тип функции. Поэтому пишут `typeof createUser`.

```typescript
type CreateUserFn = typeof createUser;
type User = ReturnType<CreateUserFn>;
```

## С async-функцией

```typescript
async function loadUser() {
  return { id: 1, name: "Анна" };
}

type LoadResult = ReturnType<typeof loadUser>;
// Promise<{ id: number; name: string }>
```

Чтобы достать значение из `Promise`, используют `Awaited`.

```typescript
type User = Awaited<ReturnType<typeof loadUser>>;
```

## Где полезен

`ReturnType` помогает не дублировать тип результата, если форма объекта уже задается функцией.

## Мини-шпаргалка

- `ReturnType<T>` достает return type функции.
- Для функции-значения нужен `typeof`.
- Для async часто пишут `Awaited<ReturnType<typeof fn>>`.
- Удобен для factory-функций и селекторов.
