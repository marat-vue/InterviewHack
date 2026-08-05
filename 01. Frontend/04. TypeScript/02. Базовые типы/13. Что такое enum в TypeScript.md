# Что такое enum в TypeScript?

> [!NOTE]
> `enum` задает набор именованных констант, но в современном TS часто вместо него используют union из литеральных типов.

## Вопрос

Что такое `enum` и когда его использовать?

## Определение

`enum` позволяет описать набор именованных значений. Он существует не только на уровне типов: обычный `enum` генерирует JavaScript-код после компиляции.

## Числовой enum

```typescript
enum Direction {
  Up,
  Down,
  Left,
  Right,
}

const direction: Direction = Direction.Up;
```

По умолчанию значения будут `0`, `1`, `2`, `3`.

## Строковый enum

```typescript
enum Role {
  Admin = 'admin',
  User = 'user',
}

const role: Role = Role.Admin;
```

Строковые enum обычно понятнее в логах и данных.

## Альтернатива через union

```typescript
type Role = 'admin' | 'user';

const role: Role = 'admin';
```

Union часто проще, легче совместим с обычными строками и не генерирует лишний JavaScript.

## enum vs union

| Подход | Особенность |
| --- | --- |
| `enum` | создает runtime-объект |
| `const enum` | может быть inline, но имеет нюансы сборки |
| union literals | только тип, без JS-кода |

## Мини-шпаргалка

```typescript
enum Status {
  Idle = 'idle',
  Loading = 'loading',
}

type StatusUnion = 'idle' | 'loading';
```
