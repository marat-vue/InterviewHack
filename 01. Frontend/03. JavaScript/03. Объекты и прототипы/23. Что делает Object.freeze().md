# `Object.freeze()`

> [!NOTE]
> `Object.freeze(obj)` замораживает объект на верхнем уровне: нельзя добавлять, удалять и менять существующие свойства. Возвращает тот же объект.

## Вопрос

Что делает `Object.freeze()`?

## Базовый пример

```javascript
const user = {
  name: "Anna",
};

Object.freeze(user);

user.name = "Max";
user.age = 25;
delete user.name;

console.log(user); // { name: "Anna" }
```

В strict mode такие операции могут выбрасывать `TypeError`.

## Что меняется в дескрипторах

`freeze` делает существующие свойства:

- `writable: false`;
- `configurable: false`.

И запрещает расширять объект.

```javascript
Object.isFrozen(user); // true
```

## Только верхний уровень

```javascript
const user = {
  profile: {
    city: "Moscow",
  },
};

Object.freeze(user);

user.profile.city = "Kazan"; // можно
```

`profile` как ссылка не меняется, но сам вложенный объект не заморожен.

## Deep freeze

Для глубокой заморозки нужно рекурсивно заморозить вложенные объекты.

```javascript
function deepFreeze(obj) {
  Object.freeze(obj);

  for (const value of Object.values(obj)) {
    if (value && typeof value === "object") {
      deepFreeze(value);
    }
  }

  return obj;
}
```

## `freeze` vs `const`

```javascript
const user = { name: "Anna" };

user.name = "Max"; // можно
```

`const` запрещает переназначить переменную, но не замораживает объект. `Object.freeze` защищает свойства объекта.

## Мини-шпаргалка

| Действие после `freeze` | Можно? |
| --- | --- |
| добавить свойство | нет |
| удалить свойство | нет |
| изменить верхнее свойство | нет |
| изменить вложенный объект | да, если он не frozen |
| переназначить переменную `const` | нет, это другое правило |
