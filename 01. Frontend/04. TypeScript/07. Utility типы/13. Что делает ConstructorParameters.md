# Что делает ConstructorParameters?

> [!NOTE]
> `ConstructorParameters<T>` достает типы параметров конструктора класса или constructor signature в виде кортежа.

## Вопрос

Что делает `ConstructorParameters`?

## Базовый пример

```typescript
class User {
  constructor(
    public name: string,
    public age: number
  ) {}
}

type UserConstructorArgs = ConstructorParameters<typeof User>;
// [name: string, age: number]
```

Для класса нужен `typeof`, потому что сам `User` как тип описывает экземпляр, а `typeof User` - конструктор.

## Wrapper для создания экземпляра

```typescript
function createUser(...args: ConstructorParameters<typeof User>): User {
  return new User(...args);
}
```

Если сигнатура конструктора изменится, wrapper обновится автоматически.

## Constructor signature

```typescript
type Constructor = new (url: string, retries?: number) => ApiClient;

type Args = ConstructorParameters<Constructor>;
// [url: string, retries?: number]
```

## Ограничение

`ConstructorParameters` работает только с типами, которые можно вызвать через `new`.

```typescript
// type Bad = ConstructorParameters<() => string>; // ошибка
```

## Мини-шпаргалка

- Достает параметры конструктора как tuple.
- Для класса пишут `ConstructorParameters<typeof ClassName>`.
- Полезен для factory и DI-контейнеров.
- Для обычных функций нужен `Parameters<T>`.
