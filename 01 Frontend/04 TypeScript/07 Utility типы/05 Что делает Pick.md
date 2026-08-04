# Что делает Pick?

> [!NOTE] Коротко
> `Pick<T, K>` создает новый тип из выбранных свойств типа `T`. Второй аргумент `K` - union ключей, которые нужно оставить.

## Вопрос

Что делает `Pick`?

## Базовый пример

```typescript
type User = {
  id: number;
  name: string;
  email: string;
  passwordHash: string;
};

type UserPreview = Pick<User, "id" | "name">;
```

`UserPreview` будет таким:

```typescript
type UserPreview = {
  id: number;
  name: string;
};
```

## Где полезен

`Pick` удобен, когда нужно отдать наружу только часть полей.

```typescript
function toPreview(user: User): Pick<User, "id" | "name"> {
  return {
    id: user.id,
    name: user.name,
  };
}
```

## Ключи проверяются

TypeScript не даст выбрать поле, которого нет в исходном типе.

```typescript
// type Bad = Pick<User, "avatar">; // ошибка
```

## Pick и keyof

Под капотом `Pick` работает с ключами объекта.

```typescript
type UserKey = keyof User;
// "id" | "name" | "email" | "passwordHash"
```

## Мини-шпаргалка

- `Pick<T, K>` оставляет только ключи `K`.
- `K` должен быть ключом `T`.
- Хорошо подходит для preview, DTO и пропсов.
- Противоположная задача решается через `Omit`.
