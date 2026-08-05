# `NaN`

> [!NOTE]
> `NaN` означает Not-a-Number, но его тип - `number`. Это специальное значение для некорректного числового результата. Проверять его лучше через `Number.isNaN()`.

## Вопрос

Что такое `NaN` и как его проверить? Почему `NaN === NaN` возвращает `false`?

## Что такое `NaN`

`NaN` появляется, когда операция должна вернуть число, но корректное число получить невозможно.

```javascript
Number("abc");    // NaN
0 / 0;            // NaN
Math.sqrt(-1);    // NaN
"hello" * 2;      // NaN
```

При этом:

```javascript
typeof NaN; // "number"
```

Это кажется странным, но логика такая: `NaN` находится внутри числового типа и обозначает неудачный числовой результат.

## Почему `NaN !== NaN`

```javascript
NaN === NaN; // false
NaN == NaN;  // false
```

По правилам IEEE 754 значение `NaN` не равно ничему, включая само себя. Это позволяет отличать неопределенный числовой результат от обычного числа.

## Как проверять

Лучший вариант:

```javascript
Number.isNaN(value);
```

Примеры:

```javascript
Number.isNaN(NaN);      // true
Number.isNaN(10);       // false
Number.isNaN("hello");  // false
Number.isNaN("10");     // false
```

Глобальный `isNaN` использовать опаснее, потому что он сначала приводит значение к числу:

```javascript
isNaN("hello"); // true, потому что Number("hello") -> NaN
isNaN("10");    // false, потому что Number("10") -> 10
```

## Еще два способа

```javascript
Object.is(NaN, NaN); // true
```

И самый необычный:

```javascript
const value = NaN;

value !== value; // true только для NaN
```

В обычном коде лучше использовать `Number.isNaN`.

## Практический пример

```javascript
function parseAge(input) {
  const age = Number(input);

  if (Number.isNaN(age)) {
    return null;
  }

  return age;
}

parseAge("25");  // 25
parseAge("abc"); // null
```

## Мини-шпаргалка

| Проверка | Результат |
| --- | --- |
| `typeof NaN` | `"number"` |
| `NaN === NaN` | `false` |
| `Number.isNaN(NaN)` | `true` |
| `Number.isNaN("abc")` | `false` |
| `isNaN("abc")` | `true` |
