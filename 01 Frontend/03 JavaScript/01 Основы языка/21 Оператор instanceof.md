# Оператор `instanceof`

> [!NOTE]
> `instanceof` проверяет, есть ли `Constructor.prototype` в цепочке прототипов объекта. Проще: создан ли объект этим конструктором или наследуется ли от него.

## Вопрос

Что делает оператор `instanceof`?

## Синтаксис

```javascript
object instanceof Constructor;
```

Пример:

```javascript
const date = new Date();

date instanceof Date;   // true
date instanceof Object; // true
```

`Date` находится в цепочке прототипов объекта `date`, а `Object` выше по этой цепочке.

## Как это работает

Когда вы пишете:

```javascript
obj instanceof User;
```

JavaScript проверяет, встречается ли `User.prototype` внутри prototype chain объекта `obj`.

```javascript
function User(name) {
  this.name = name;
}

const anna = new User("Anna");

anna instanceof User;   // true
anna instanceof Object; // true
```

## С классами

С классами работает так же, потому что классы в JavaScript построены поверх прототипов.

```javascript
class Animal {}
class Dog extends Animal {}

const dog = new Dog();

dog instanceof Dog;    // true
dog instanceof Animal; // true
dog instanceof Object; // true
```

## Где полезно

`instanceof` часто используют, чтобы проверить конкретный тип объекта:

```javascript
function formatError(error) {
  if (error instanceof Error) {
    return error.message;
  }

  return String(error);
}
```

## Подводные камни

### Примитивы не являются экземплярами оберток

```javascript
"hello" instanceof String; // false
new String("hello") instanceof String; // true
```

Обычная строка - примитив, а `new String()` создает объект-обертку.

### Разные окна браузера

Объекты из разных iframe могут иметь разные конструкторы.

```javascript
arrayFromIframe instanceof Array; // может быть false
```

Для массивов надежнее:

```javascript
Array.isArray(value);
```

## Мини-шпаргалка

| Выражение | Результат |
| --- | --- |
| `new Date() instanceof Date` | `true` |
| `new Date() instanceof Object` | `true` |
| `[] instanceof Array` | `true` |
| `[] instanceof Object` | `true` |
| `"x" instanceof String` | `false` |
