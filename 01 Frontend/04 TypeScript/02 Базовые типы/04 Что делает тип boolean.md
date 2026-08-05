# Что делает тип boolean?

> [!NOTE]
> `boolean` описывает логические значения `true` и `false`.

## Вопрос

Для чего нужен тип `boolean` в TypeScript?

## Определение

`boolean` используют для флагов, условий, состояний интерфейса и результатов проверок. Значение такого типа может быть только `true` или `false`.

## Пример

```typescript
let isLoading: boolean = true;
let isAdmin: boolean = false;
```

## Результат сравнения

```typescript
const age = 18;
const canVote: boolean = age >= 18;
```

Операции сравнения возвращают boolean.

## Ошибка типа

```typescript
let isVisible: boolean = true;

isVisible = 'yes'; // ошибка TypeScript
```

Строка `'yes'` не является boolean.

## Boolean literal types

```typescript
type AlwaysTrue = true;

const value: AlwaysTrue = true;
```

Иногда полезно описывать конкретное логическое значение, особенно в union-типах.

## Не путать с Boolean

```typescript
let flag: boolean = false; // правильно
let objectFlag: Boolean = new Boolean(false); // почти всегда не нужно
```

Объект `Boolean` может вести себя неожиданно в условиях, потому что любой объект truthy.

## Мини-шпаргалка

```typescript
let flag: boolean = true;
const isValid: boolean = value !== null;
```
