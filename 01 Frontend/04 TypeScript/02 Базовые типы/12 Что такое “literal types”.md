# Что такое “literal types”?

> [!NOTE]
> Literal type описывает не общий тип вроде `string`, а конкретное значение: `'dark'`, `42` или `true`.

## Вопрос

Что такое литеральные типы в TypeScript?

## Определение

Литеральный тип - тип, который допускает только одно конкретное значение. Чаще всего литеральные типы объединяют в union, чтобы описать набор допустимых вариантов.

## String literal types

```typescript
type Theme = 'light' | 'dark';

let theme: Theme = 'light';

theme = 'dark';
theme = 'blue'; // ошибка
```

## Number literal types

```typescript
type Dice = 1 | 2 | 3 | 4 | 5 | 6;

const roll: Dice = 6;
```

## Boolean literal types

```typescript
type Success = true;

const ok: Success = true;
```

## Практический пример

```typescript
type RequestState = 'idle' | 'loading' | 'success' | 'error';

function render(state: RequestState) {
  if (state === 'loading') {
    return 'Loading...';
  }
}
```

Такой тип защищает от опечаток и запрещает неизвестные состояния.

## as const

```typescript
const config = {
  theme: 'dark',
} as const;
```

`as const` делает значения максимально узкими и неизменяемыми на уровне типов.

## Мини-шпаргалка

```typescript
type Size = 'sm' | 'md' | 'lg';
type StatusCode = 200 | 400 | 500;
```
