# Метод `toJSON()`

> [!NOTE] Коротко
> `toJSON()` - специальный метод, который автоматически вызывается при `JSON.stringify()`. В JSON попадает результат `toJSON()`, а не исходный объект.

## Вопрос

Что делает метод `toJSON()`?

## Базовый пример

```javascript
const user = {
  name: "Anna",
  password: "secret",

  toJSON() {
    return {
      name: this.name,
    };
  },
};

JSON.stringify(user); // '{"name":"Anna"}'
```

Метод позволяет контролировать сериализацию.

## Где применяется

`toJSON()` полезен, чтобы:

- скрыть приватные поля;
- изменить формат данных;
- убрать циклические ссылки;
- сериализовать только нужные свойства;
- подготовить объект к API.

## Вложенные объекты

```javascript
const data = {
  user: {
    name: "Anna",
    password: "secret",
    toJSON() {
      return { name: this.name };
    },
  },
};

JSON.stringify(data); // '{"user":{"name":"Anna"}}'
```

Если вложенный объект имеет `toJSON`, он тоже будет вызван.

## `Date.toJSON`

У `Date` уже есть встроенный `toJSON`.

```javascript
const date = new Date("2026-01-01T00:00:00.000Z");

JSON.stringify({ date });
// '{"date":"2026-01-01T00:00:00.000Z"}'
```

Дата превращается в ISO-строку.

## Порядок работы

При `JSON.stringify(value, replacer)`:

1. если есть `toJSON`, вызывается он;
2. затем применяется `replacer`;
3. затем значение сериализуется.

## `JSON.parse` не использует `toJSON`

```javascript
JSON.parse(json);
```

`toJSON` работает только при сериализации, не при чтении JSON. Для преобразования при `parse` используют `reviver`.

## Мини-шпаргалка

| Метод | Когда работает |
| --- | --- |
| `toJSON()` | при `JSON.stringify` |
| `replacer` | после `toJSON` |
| `reviver` | при `JSON.parse` |
| `Date.prototype.toJSON` | возвращает ISO-строку |
