# Что делает Partial?

> [!NOTE] Коротко
> `Partial<T>` делает все свойства типа `T` опциональными. Это удобно для черновиков, обновлений и объектов с частично заполненными данными.

## Вопрос

Что делает `Partial`?

## Базовый пример

```typescript
type User = {
  id: number;
  name: string;
  email: string;
};

type UserPatch = Partial<User>;
```

`UserPatch` эквивалентен такому типу:

```typescript
type UserPatch = {
  id?: number;
  name?: string;
  email?: string;
};
```

## Где полезен

Частый пример - функция обновления, где можно передать только изменившиеся поля.

```typescript
function updateUser(id: number, patch: Partial<User>): User {
  return {
    id,
    name: patch.name ?? "Без имени",
    email: patch.email ?? "unknown@example.com",
  };
}
```

## Важный нюанс

`Partial` делает опциональными только верхнеуровневые поля. Вложенные объекты не становятся глубоким `Partial`.

```typescript
type Profile = {
  user: {
    name: string;
    age: number;
  };
};

type Draft = Partial<Profile>;
// user?: { name: string; age: number }
```

## Мини-шпаргалка

- `Partial<T>` превращает поля `T` в optional.
- Подходит для patch/update DTO.
- Работает поверхностно.
- Не удаляет типы значений, а добавляет возможность отсутствия поля.
