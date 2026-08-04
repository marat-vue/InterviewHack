# Оператор `typeof`

> [!NOTE] Коротко
> `typeof` в JavaScript возвращает строку с типом значения во время выполнения. Он полезен для простых проверок, но имеет особенности: `typeof null` дает `"object"`, а массивы тоже дают `"object"`.

## Вопрос

Что возвращает оператор `typeof`? Чем он отличается от оператора `typeof` в TypeScript?

## `typeof` в JavaScript

`typeof` - унарный оператор. Он принимает значение и возвращает строку.

```javascript
typeof 42;          // "number"
typeof "hello";     // "string"
typeof true;        // "boolean"
typeof undefined;   // "undefined"
typeof 10n;         // "bigint"
typeof Symbol("x"); // "symbol"
typeof {};          // "object"
typeof function () {} // "function"
```

## Особенности

### `null`

```javascript
typeof null; // "object"
```

Это историческая ошибка языка. Для проверки `null` используйте строгое сравнение:

```javascript
value === null;
```

### Массивы

```javascript
typeof []; // "object"
```

Массивы проверяют так:

```javascript
Array.isArray(value);
```

### Необъявленные переменные

`typeof` не падает на необъявленной переменной:

```javascript
typeof notDeclared; // "undefined"
```

Это бывает полезно для безопасных проверок окружения.

## Пример практической проверки

```javascript
function formatPrice(price) {
  if (typeof price !== "number" || Number.isNaN(price)) {
    return "Некорректная цена";
  }

  return `${price} ₽`;
}
```

## `typeof` в TypeScript

В TypeScript у `typeof` две роли.

В обычном коде он работает как в JavaScript:

```typescript
const count = 5;
console.log(typeof count); // "number"
```

В позиции типа он извлекает тип существующей переменной:

```typescript
const user = {
  id: 1,
  name: "Anna",
};

type User = typeof user;
// type User = { id: number; name: string }
```

Частый пример:

```typescript
function createUser() {
  return { id: 1, name: "Anna" };
}

type User = ReturnType<typeof createUser>;
```

## Мини-шпаргалка

| Значение | `typeof` |
| --- | --- |
| `123` | `"number"` |
| `"abc"` | `"string"` |
| `true` | `"boolean"` |
| `undefined` | `"undefined"` |
| `null` | `"object"` |
| `[]` | `"object"` |
| `{}` | `"object"` |
| `() => {}` | `"function"` |
