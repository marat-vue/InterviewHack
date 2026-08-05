# `instanceof` и прототипы

> [!NOTE]
> `obj instanceof Constructor` возвращает `true`, если `Constructor.prototype` встречается в цепочке прототипов объекта `obj`.

## Вопрос

Что делает `instanceof` и как он использует прототипы?

## Синтаксис

```javascript
obj instanceof Constructor;
```

Пример:

```javascript
function User(name) {
  this.name = name;
}

const user = new User("Anna");

user instanceof User;   // true
user instanceof Object; // true
```

## Как проверяет

```javascript
Object.getPrototypeOf(user) === User.prototype; // true
```

`instanceof` поднимается по цепочке:

```text
user -> User.prototype -> Object.prototype -> null
```

Если находит `User.prototype`, возвращает `true`.

## С классами

```javascript
class Animal {}
class Dog extends Animal {}

const dog = new Dog();

dog instanceof Dog;    // true
dog instanceof Animal; // true
dog instanceof Object; // true
```

Наследование строит цепочку прототипов, поэтому все три проверки true.

## Ручная модель

```javascript
function instanceOf(obj, Constructor) {
  let proto = Object.getPrototypeOf(obj);

  while (proto !== null) {
    if (proto === Constructor.prototype) return true;
    proto = Object.getPrototypeOf(proto);
  }

  return false;
}
```

## Подводные камни

Между разными iframe/window у встроенных конструкторов могут быть разные прототипы.

```javascript
arrayFromIframe instanceof Array; // может быть false
```

Для массивов лучше:

```javascript
Array.isArray(value);
```

Для примитивов:

```javascript
"hello" instanceof String; // false
```

## Мини-шпаргалка

| Выражение | Смысл |
| --- | --- |
| `obj instanceof Ctor` | есть ли `Ctor.prototype` в цепочке |
| `Object.getPrototypeOf(obj)` | следующий прототип |
| `new Ctor()` | связывает объект с `Ctor.prototype` |
| `Array.isArray(value)` | надежнее для массивов |
