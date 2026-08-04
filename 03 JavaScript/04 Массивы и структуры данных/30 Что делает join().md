# `join()`

> [!NOTE] Коротко
> `join()` объединяет элементы массива в строку, вставляя между ними указанный разделитель. Исходный массив не изменяется.

## Вопрос

Что делает `join()`?

## Пример

```javascript
const fruits = ["apple", "banana", "cherry"];

fruits.join(", "); // "apple, banana, cherry"
```

## Разделитель

```javascript
["a", "b", "c"].join("-"); // "a-b-c"
["a", "b", "c"].join("");  // "abc"
```

Если разделитель не передать, используется запятая.

```javascript
["a", "b", "c"].join(); // "a,b,c"
```

## `null` и `undefined`

`null` и `undefined` превращаются в пустую строку.

```javascript
["a", null, undefined, "b"].join("-");
// "a---b"
```

## Пустой массив

```javascript
[].join(","); // ""
```

## Частый паттерн

```javascript
const classNames = ["button", isActive && "button_active"]
  .filter(Boolean)
  .join(" ");
```

Так можно собирать строку классов.

## Мини-шпаргалка

| Код | Результат |
| --- | --- |
| `arr.join()` | строка через запятую |
| `arr.join(" ")` | строка через пробел |
| `arr.join("")` | склейка без разделителя |
| `[].join(",")` | `""` |
| `[null].join()` | `""` |
