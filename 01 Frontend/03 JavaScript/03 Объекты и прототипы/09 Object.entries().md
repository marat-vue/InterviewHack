# `Object.entries()`

> [!NOTE]
> `Object.entries(obj)` возвращает массив пар `[key, value]` для собственных перечисляемых свойств объекта.

## Вопрос

Что делает `Object.entries()`?

## Базовый пример

```javascript
const user = {
  name: "Anna",
  age: 25,
};

Object.entries(user);
// [["name", "Anna"], ["age", 25]]
```

Каждый элемент результата - массив из ключа и значения.

## Удобный перебор

```javascript
for (const [key, value] of Object.entries(user)) {
  console.log(key, value);
}
```

Деструктуризация делает код читаемым.

## Только own enumerable

```javascript
const proto = { role: "user" };
const user = Object.create(proto);
user.name = "Anna";

Object.entries(user); // [["name", "Anna"]]
```

Свойства прототипа и неперечисляемые свойства не попадут в результат.

## Преобразование объекта

```javascript
const prices = {
  apple: 100,
  banana: 80,
};

const withDiscount = Object.fromEntries(
  Object.entries(prices).map(([name, price]) => [name, price * 0.9])
);

// { apple: 90, banana: 72 }
```

`Object.entries` часто используют вместе с `map/filter` и `Object.fromEntries`.

## Мини-шпаргалка

```javascript
Object.entries({ a: 1, b: 2 });
// [["a", 1], ["b", 2]]

for (const [key, value] of Object.entries(obj)) {}

Object.fromEntries(entries);
```

| Метод | Результат |
| --- | --- |
| `Object.keys(obj)` | `["a", "b"]` |
| `Object.values(obj)` | `[1, 2]` |
| `Object.entries(obj)` | `[["a", 1], ["b", 2]]` |
