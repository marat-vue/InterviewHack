# `this` в JavaScript

> [!NOTE] Коротко
> `this` - это контекст вызова функции. В обычных функциях он определяется способом вызова, а в стрелочных функциях берется из внешней области.

## Вопрос

Что такое `this` в JavaScript?

## Главное правило

`this` определяется в момент вызова.

```javascript
function showThis() {
  console.log(this);
}
```

Одна и та же функция может получить разный `this`.

## Обычный вызов

```javascript
function fn() {
  return this;
}

fn(); // undefined в strict mode
```

Без strict mode в браузерном скрипте `this` может быть `window`.

## Метод объекта

```javascript
const user = {
  name: "Anna",
  sayHi() {
    return `Hi, ${this.name}`;
  },
};

user.sayHi(); // "Hi, Anna"
```

`this` указывает на объект слева от точки.

## Потеря контекста

```javascript
const sayHi = user.sayHi;

sayHi(); // this уже не user
```

Функция вызвана отдельно, а не как `user.sayHi()`.

## Явная привязка

```javascript
function sayHi() {
  return `Hi, ${this.name}`;
}

sayHi.call({ name: "Anna" }); // "Hi, Anna"
```

Также есть `apply` и `bind`.

## Вызов через `new`

```javascript
function User(name) {
  this.name = name;
}

const user = new User("Anna");
```

При `new` создается новый объект, и `this` внутри конструктора указывает на него.

## Стрелочная функция

```javascript
const user = {
  name: "Anna",
  sayHi: () => this.name,
};
```

Стрелочная функция не имеет собственного `this`, поэтому такой метод обычно ошибка.

Хороший случай для стрелки:

```javascript
function Timer() {
  this.seconds = 0;

  setInterval(() => {
    this.seconds++;
  }, 1000);
}
```

Стрелка берет `this` из `Timer`.

## Мини-шпаргалка

| Вызов | Значение `this` |
| --- | --- |
| `fn()` | `undefined` в strict mode |
| `obj.fn()` | `obj` |
| `fn.call(obj)` | `obj` |
| `fn.apply(obj)` | `obj` |
| `fn.bind(obj)` | закрепленный `obj` |
| `new Fn()` | новый объект |
| arrow function | внешний `this` |
