# `Object.create()`

> [!NOTE] Коротко
> `Object.create(proto)` создает новый объект с явно заданным прототипом. Прототипом может быть объект или `null`.

## Вопрос

Что делает `Object.create()`?

## Синтаксис

```javascript
Object.create(proto, propertiesObject);
```

`propertiesObject` необязателен и задает свойства через дескрипторы.

## Базовый пример

```javascript
const userProto = {
  sayHi() {
    return `Hi, ${this.name}`;
  },
};

const user = Object.create(userProto);
user.name = "Anna";

user.sayHi(); // "Hi, Anna"
```

Метод `sayHi` находится в прототипе, а `name` - собственное свойство объекта.

## Проверка прототипа

```javascript
Object.getPrototypeOf(user) === userProto; // true
```

## Объект без прототипа

```javascript
const dict = Object.create(null);

Object.getPrototypeOf(dict); // null
```

У такого объекта нет `toString`, `constructor`, `hasOwnProperty`.

```javascript
dict.toString; // undefined
```

Это иногда удобно для словарей без унаследованных ключей.

## Создание свойств через descriptor

```javascript
const user = Object.create(userProto, {
  name: {
    value: "Anna",
    enumerable: true,
    writable: true,
  },
});
```

Это похоже на `Object.defineProperty`.

## Мини-шпаргалка

| Код | Результат |
| --- | --- |
| `Object.create(proto)` | объект с прототипом `proto` |
| `Object.create(null)` | объект без прототипа |
| `Object.getPrototypeOf(obj)` | получить прототип |
| `Object.create(proto, descriptors)` | создать + описать свойства |
