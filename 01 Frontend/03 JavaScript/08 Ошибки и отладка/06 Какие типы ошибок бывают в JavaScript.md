# Какие типы ошибок бывают в JavaScript?

> [!NOTE]
> В JavaScript есть базовый `Error` и встроенные типы ошибок: `TypeError`, `ReferenceError`, `SyntaxError`, `RangeError` и другие.

## Вопрос

Какие встроенные типы ошибок есть в JavaScript?

## Основные типы

| Тип | Когда возникает |
| --- | --- |
| `Error` | базовый тип ошибки |
| `TypeError` | операция применена к неподходящему типу |
| `ReferenceError` | обращение к несуществующей переменной |
| `SyntaxError` | некорректный синтаксис или парсинг |
| `RangeError` | значение вне допустимого диапазона |
| `URIError` | ошибка в URI-функциях |
| `AggregateError` | несколько ошибок сразу |

## TypeError

```javascript
const user = null;

console.log(user.name); // TypeError
```

## ReferenceError

```javascript
console.log(notDeclared); // ReferenceError
```

## SyntaxError

```javascript
JSON.parse('{ broken json }'); // SyntaxError
```

Здесь ошибка возникает во время выполнения `JSON.parse`, поэтому ее можно поймать через `try...catch`.

## RangeError

```javascript
const numbers = new Array(-1); // RangeError
```

## AggregateError

```javascript
try {
  await Promise.any([
    Promise.reject(new Error('A')),
    Promise.reject(new Error('B')),
  ]);
} catch (error) {
  console.log(error instanceof AggregateError); // true
}
```

## Мини-шпаргалка

```javascript
throw new TypeError('Expected string');
throw new RangeError('Value is too small');
throw new Error('Common error');
```
