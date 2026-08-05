# Что делает Parameters?

> [!NOTE]
> `Parameters<T>` достает типы параметров функции `T` в виде кортежа.

## Вопрос

Что делает `Parameters`?

## Базовый пример

```typescript
function createUser(name: string, age: number) {
  return { name, age };
}

type CreateUserParams = Parameters<typeof createUser>;
// [name: string, age: number]
```

Результат - tuple, потому что у параметров есть порядок.

## Использование с rest

```typescript
function callCreateUser(...args: Parameters<typeof createUser>) {
  return createUser(...args);
}
```

Так wrapper-функция автоматически повторяет параметры исходной функции.

## Достать отдельный параметр

```typescript
type FirstParam = Parameters<typeof createUser>[0];
// string
```

## С типом функции

```typescript
type Handler = (event: MouseEvent, index: number) => void;

type HandlerParams = Parameters<Handler>;
// [event: MouseEvent, index: number]
```

## Мини-шпаргалка

- `Parameters<T>` возвращает tuple параметров.
- Для функции-значения используй `typeof`.
- Удобен для wrapper-ов и повторного использования сигнатур.
- Для результата функции есть `ReturnType<T>`.
