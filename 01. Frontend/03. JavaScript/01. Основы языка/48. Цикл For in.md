# Цикл `for...in`

> [!NOTE]
> `for...in` перебирает ключи перечисляемых свойств объекта, включая унаследованные. Для массивов обычно лучше использовать `for`, `for...of` или методы массивов.

## Вопрос

Чем `for...in` отличается от `for...of`?

## `for...in`

```javascript
const user = {
  name: "Anna",
  age: 25,
};

for (const key in user) {
  console.log(key, user[key]);
}
```

Результат:

```text
name Anna
age 25
```

`for...in` перебирает ключи, а не значения.

## Унаследованные свойства

```javascript
const proto = { role: "user" };
const user = Object.create(proto);
user.name = "Anna";

for (const key in user) {
  console.log(key);
}
```

Цикл может вывести и `name`, и `role`.

Чтобы брать только собственные свойства:

```javascript
for (const key in user) {
  if (Object.hasOwn(user, key)) {
    console.log(key, user[key]);
  }
}
```

## Почему не для массивов

```javascript
const items = ["a", "b"];

for (const index in items) {
  console.log(index); // "0", "1"
}
```

Индексы приходят как строки. Кроме того, `for...in` может перебрать добавленные свойства.

```javascript
items.custom = "value";
```

Для массивов лучше:

```javascript
for (const item of items) {
  console.log(item);
}
```

## `for...in` vs `for...of`

```javascript
const items = ["a", "b"];

for (const key in items) {
  console.log(key); // "0", "1"
}

for (const value of items) {
  console.log(value); // "a", "b"
}
```

## Мини-шпаргалка

| Цикл | Что дает | Где использовать |
| --- | --- | --- |
| `for...in` | ключи | объекты |
| `for...of` | значения | iterable: массивы, строки, Set, Map |
| `Object.keys(obj)` | массив собственных ключей | современный явный вариант |
| `Object.entries(obj)` | пары `[key, value]` | удобно для объектов |
