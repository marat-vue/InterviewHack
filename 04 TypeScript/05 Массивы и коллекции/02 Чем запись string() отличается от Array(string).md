# Чем запись string[] отличается от Array?

> [!NOTE] Коротко
> `string[]` и `Array<string>` описывают один и тот же тип: массив строк. Разница только в форме записи.

## Вопрос

Чем запись `string[]` отличается от `Array<string>`?

## Короткий ответ

Ничем по смыслу. TypeScript воспринимает обе записи как массив строк.

```typescript
const a: string[] = ["html", "css"];
const b: Array<string> = ["js", "ts"];
```

## Когда удобнее `T[]`

Короткая запись хорошо читается для простых типов.

```typescript
const numbers: number[] = [1, 2, 3];
const flags: boolean[] = [true, false];
const users: User[] = [];
```

## Когда удобнее `Array<T>`

Generic-запись иногда понятнее для сложных типов.

```typescript
const values: Array<string | number> = ["id", 10];
const responses: Array<Promise<User>> = [];
const rows: Array<{ id: number; title: string }> = [];
```

## Readonly-варианты

```typescript
const a: readonly string[] = ["admin", "user"];
const b: ReadonlyArray<string> = ["admin", "user"];
```

Оба варианта запрещают менять массив.

## Мини-шпаргалка

- `T[]` и `Array<T>` эквивалентны.
- Для простых массивов обычно пишут `T[]`.
- Для длинных generic-комбинаций иногда читаемее `Array<T>`.
- `readonly T[]` и `ReadonlyArray<T>` тоже близки по смыслу.
