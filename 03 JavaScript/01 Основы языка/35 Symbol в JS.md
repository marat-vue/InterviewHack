# `Symbol` в JavaScript

> [!NOTE] Коротко
> `Symbol` - примитивный тип для создания уникальных значений. Чаще всего символы используют как ключи свойств, которые не конфликтуют с обычными строковыми ключами.

## Вопрос

Что такое `Symbol` и для чего он используется?

## Создание

```javascript
const id = Symbol("id");
```

Строка `"id"` - это описание для отладки, а не имя символа.

```javascript
const a = Symbol("id");
const b = Symbol("id");

a === b; // false
```

Каждый вызов `Symbol()` создает новое уникальное значение.

## Символ как ключ объекта

```javascript
const id = Symbol("id");

const user = {
  name: "Anna",
  [id]: 123,
};

console.log(user[id]); // 123
```

Такой ключ не конфликтует со строковыми ключами.

```javascript
const obj = {};

obj.id = "string key";
obj[Symbol("id")] = "symbol key";
```

## Символьные свойства менее заметны

Они не попадают в обычный перебор:

```javascript
const id = Symbol("id");
const user = {
  name: "Anna",
  [id]: 123,
};

Object.keys(user); // ["name"]
```

Но их можно получить отдельно:

```javascript
Object.getOwnPropertySymbols(user); // [Symbol(id)]
```

## Глобальный реестр символов

`Symbol.for()` возвращает символ из глобального реестра.

```javascript
const a = Symbol.for("app.id");
const b = Symbol.for("app.id");

a === b; // true
```

Для обычных уникальных ключей чаще нужен `Symbol()`, а не `Symbol.for()`.

## Well-known symbols

В JavaScript есть встроенные символы, которые позволяют настраивать поведение объектов.

Например, `Symbol.iterator` делает объект итерируемым:

```javascript
const range = {
  from: 1,
  to: 3,
  [Symbol.iterator]() {
    let current = this.from;
    const end = this.to;

    return {
      next() {
        if (current <= end) {
          return { value: current++, done: false };
        }

        return { done: true };
      },
    };
  },
};

[...range]; // [1, 2, 3]
```

## Подводные камни

Символ нельзя неявно склеить со строкой:

```javascript
const id = Symbol("id");

"key: " + id; // TypeError
```

Нужно явно:

```javascript
String(id); // "Symbol(id)"
```

## Мини-шпаргалка

| Выражение | Результат |
| --- | --- |
| `Symbol("id") === Symbol("id")` | `false` |
| `Symbol.for("id") === Symbol.for("id")` | `true` |
| `typeof Symbol("id")` | `"symbol"` |
| `Object.keys(obj)` | не показывает symbol-ключи |
| `Object.getOwnPropertySymbols(obj)` | показывает symbol-ключи |
