# type inference c generics

> [!NOTE] Коротко
> Type inference с generics означает, что TypeScript часто сам подставляет generic-тип по переданным аргументам. Поэтому `identity("hi")` становится `identity<string>("hi")` без явной записи.

## Вопрос

Как работает `type inference` с generics?

## Базовый пример

```typescript
function identity<T>(value: T): T {
  return value;
}

const text = identity("hello"); // string
const count = identity(10); // number
```

TypeScript смотрит на аргумент и выводит `T`.

## Вывод по массиву

```typescript
function first<T>(items: T[]): T | undefined {
  return items[0];
}

const value = first(["html", "css"]);
// string | undefined
```

## Вывод по нескольким аргументам

```typescript
function merge<T, U>(left: T, right: U): T & U {
  return { ...left, ...right };
}

const user = merge({ id: 1 }, { name: "Анна" });
// { id: number } & { name: string }
```

## Когда нужно указать тип явно

Иногда TypeScript не может вывести желаемый тип из аргументов.

```typescript
function createEmpty<T>(): T[] {
  return [];
}

const users = createEmpty<User>();
```

Аргументов нет, поэтому `T` неоткуда вывести.

## Мини-шпаргалка

- TS выводит generic по аргументам.
- Явно писать `<T>` часто не нужно.
- Если аргументов нет или тип слишком широкий, укажи generic вручную.
- Хорошая generic-функция сохраняет связь между входом и выходом.
