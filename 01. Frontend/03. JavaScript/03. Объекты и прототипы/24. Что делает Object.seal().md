# `Object.seal()`

> [!NOTE]
> `Object.seal(obj)` запечатывает объект: нельзя добавлять и удалять свойства, но можно менять значения существующих свойств, если они `writable: true`.

## Вопрос

Что делает `Object.seal()`?

## Базовый пример

```javascript
const user = {
  name: "Anna",
};

Object.seal(user);

user.name = "Max"; // можно
user.age = 25;     // нельзя добавить
delete user.name;  // нельзя удалить

console.log(user); // { name: "Max" }
```

## Что меняется

`Object.seal`:

- запрещает добавлять новые свойства;
- запрещает удалять существующие свойства;
- делает свойства `configurable: false`;
- не делает их автоматически `writable: false`.

Проверка:

```javascript
Object.isSealed(user); // true
```

## Отличие от `freeze`

```javascript
const user = { name: "Anna" };

Object.seal(user);
user.name = "Max"; // можно
```

```javascript
const user = { name: "Anna" };

Object.freeze(user);
user.name = "Max"; // нельзя
```

`freeze` строже: он еще запрещает менять значения.

## Отличие от `preventExtensions`

`preventExtensions` запрещает только добавление новых свойств.

```javascript
Object.preventExtensions(user);

delete user.name; // можно
```

`seal` запрещает и добавление, и удаление.

## Мини-шпаргалка

| Операция после `seal` | Можно? |
| --- | --- |
| добавить свойство | нет |
| удалить свойство | нет |
| изменить существующее writable-свойство | да |
| изменить descriptor | обычно нет |
| проверить | `Object.isSealed(obj)` |
