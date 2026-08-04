# Что такое тип number?

> [!NOTE] Коротко
> `number` описывает числовые значения JavaScript: целые, дробные, `NaN`, `Infinity` и `-Infinity`.

## Вопрос

Что входит в тип `number` в TypeScript?

## Определение

`number` - примитивный тип для чисел. В JavaScript нет отдельного типа для integer и float: большинство чисел представлены одним типом `number`.

## Пример

```typescript
let age: number = 25;
let price: number = 199.99;
let temperature: number = -10;
```

## Ошибка типа

```typescript
let count: number = 10;

count = '10'; // ошибка TypeScript
```

## Специальные числовые значения

```typescript
const notNumber: number = NaN;
const positiveInfinity: number = Infinity;
const negativeInfinity: number = -Infinity;
```

Они тоже относятся к типу `number`.

## Числовые литеральные типы

```typescript
type Dice = 1 | 2 | 3 | 4 | 5 | 6;

let roll: Dice = 6;
roll = 10; // ошибка
```

Литеральные типы позволяют ограничить допустимые числа.

## number vs bigint

```typescript
const small: number = 100;
const big: bigint = 100n;
```

`number` и `bigint` нельзя свободно смешивать в арифметике.

## Мини-шпаргалка

```typescript
let n: number = 42;
let x: number = 3.14;
let bad: number = NaN;
```
