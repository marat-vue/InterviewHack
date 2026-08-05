# `JSON.stringify()`

> [!NOTE]
> `JSON.stringify(value)` преобразует JavaScript-значение в JSON-строку. Это называют сериализацией.

## Вопрос

Что делает `JSON.stringify()`?

## Базовый пример

```javascript
const user = {
  name: "Anna",
  age: 25,
};

const json = JSON.stringify(user);

console.log(json); // '{"name":"Anna","age":25}'
```

## Синтаксис

```javascript
JSON.stringify(value, replacer, space);
```

- `value` - что сериализуем;
- `replacer` - фильтрация или преобразование;
- `space` - отступы для красивого JSON.

## Красивый вывод

```javascript
JSON.stringify(user, null, 2);
```

Результат:

```json
{
  "name": "Anna",
  "age": 25
}
```

## Что пропадает

В объектах пропускаются:

```javascript
JSON.stringify({
  a: undefined,
  b: function () {},
  c: Symbol("c"),
});
// "{}"
```

В массивах такие значения превращаются в `null`.

```javascript
JSON.stringify([undefined, function () {}, Symbol("x")]);
// "[null,null,null]"
```

## `replacer`

Массив ключей:

```javascript
JSON.stringify(user, ["name"]);
// '{"name":"Anna"}'
```

Функция:

```javascript
JSON.stringify(user, (key, value) => {
  if (key === "password") return undefined;
  return value;
});
```

## `toJSON`

Если у объекта есть `toJSON`, сначала вызывается он.

```javascript
const user = {
  name: "Anna",
  password: "secret",
  toJSON() {
    return { name: this.name };
  },
};

JSON.stringify(user); // '{"name":"Anna"}'
```

## Мини-шпаргалка

| Значение | Поведение |
| --- | --- |
| object/array | сериализуется |
| `undefined` в объекте | пропускается |
| `undefined` в массиве | `null` |
| function | пропускается или `null` в массиве |
| `Symbol` | пропускается или `null` в массиве |
| циклическая ссылка | `TypeError` |
| `BigInt` | `TypeError` |
