# Что хранится в `__proto__`?

> [!NOTE]
> `__proto__` - исторический accessor к внутренней ссылке `[[Prototype]]` объекта. Он указывает на прототип, от которого объект наследует свойства.

## Вопрос

Что хранится в `__proto__`?

## Пример

```javascript
const user = {};

user.__proto__ === Object.prototype; // true
Object.prototype.__proto__;          // null
```

`__proto__` показывает прототип объекта.

## Современный способ

Лучше использовать:

```javascript
Object.getPrototypeOf(user);
```

И для изменения:

```javascript
Object.setPrototypeOf(user, proto);
```

Но менять прототип существующего объекта обычно не рекомендуется из-за производительности и читаемости.

## Не путать с `prototype`

```javascript
function User() {}

const user = new User();

user.__proto__ === User.prototype; // true
```

`User.prototype` - объект, который станет прототипом экземпляров.

`user.__proto__` - фактический прототип конкретного объекта.

## Как работает поиск

```javascript
const proto = { role: "user" };
const user = Object.create(proto);

user.role; // "user"
```

Если `role` нет в `user`, JavaScript идет в `user.__proto__`.

## Почему осторожно

`__proto__` существует ради совместимости. В учебных примерах его часто показывают, но в рабочем коде предпочтительнее:

```javascript
Object.getPrototypeOf(obj);
Object.create(proto);
```

## Мини-шпаргалка

| Запись | Значение |
| --- | --- |
| `obj.__proto__` | прототип объекта |
| `Object.getPrototypeOf(obj)` | современное чтение прототипа |
| `Ctor.prototype` | прототип будущих экземпляров |
| `obj.__proto__ === Ctor.prototype` | часто true после `new Ctor()` |
