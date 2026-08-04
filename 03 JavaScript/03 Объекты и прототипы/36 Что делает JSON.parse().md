# `JSON.parse()`

> [!NOTE] Коротко
> `JSON.parse(json)` преобразует JSON-строку в JavaScript-значение. Если строка не является валидным JSON, будет `SyntaxError`.

## Вопрос

Что делает `JSON.parse()`?

## Базовый пример

```javascript
const json = '{"name":"Anna","age":25}';
const user = JSON.parse(json);

console.log(user.name); // "Anna"
```

JSON-строка превратилась в объект JavaScript.

## Что можно распарсить

```javascript
JSON.parse('{"a":1}'); // object
JSON.parse("[1,2,3]"); // array
JSON.parse('"hello"'); // string
JSON.parse("123");     // number
JSON.parse("true");    // boolean
JSON.parse("null");    // null
```

## Только валидный JSON

Так нельзя:

```javascript
JSON.parse("{name: 'Anna'}"); // SyntaxError
```

Проблемы:

- ключ без двойных кавычек;
- строка в одинарных кавычках.

Trailing comma тоже нельзя:

```javascript
JSON.parse('{"name":"Anna",}'); // SyntaxError
```

## Обработка ошибок

```javascript
function safeParse(json) {
  try {
    return JSON.parse(json);
  } catch (error) {
    return null;
  }
}
```

`JSON.parse` часто оборачивают в `try...catch`, если строка приходит извне.

## `reviver`

Второй аргумент позволяет преобразовать значения.

```javascript
const json = '{"name":"Anna","createdAt":"2026-01-01T00:00:00.000Z"}';

const user = JSON.parse(json, (key, value) => {
  if (key === "createdAt") {
    return new Date(value);
  }

  return value;
});

user.createdAt instanceof Date; // true
```

## Мини-шпаргалка

| Код | Результат |
| --- | --- |
| `JSON.parse("{}")` | объект |
| `JSON.parse("[]")` | массив |
| `JSON.parse("true")` | boolean |
| `JSON.parse("null")` | `null` |
| невалидный JSON | `SyntaxError` |
| `JSON.parse(json, reviver)` | парсинг с преобразованием |
