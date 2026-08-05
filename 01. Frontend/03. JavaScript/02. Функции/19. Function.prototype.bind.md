# `Function.prototype.bind`

> [!NOTE]
> `bind()` не вызывает функцию сразу. Он возвращает новую функцию с заранее привязанным `this` и, при необходимости, частью аргументов.

## Вопрос

Что делает `Function.prototype.bind`?

## Синтаксис

```javascript
const boundFn = fn.bind(thisArg, arg1, arg2, ...);
```

## Привязка `this`

```javascript
const user = {
  name: "Anna",
  sayHi() {
    return `Hi, ${this.name}`;
  },
};

const sayHi = user.sayHi;
sayHi(); // this потерян
```

Исправление:

```javascript
const sayHi = user.sayHi.bind(user);

sayHi(); // "Hi, Anna"
```

## Частичное применение аргументов

```javascript
function multiply(a, b) {
  return a * b;
}

const double = multiply.bind(null, 2);

double(5); // 10
```

Первый аргумент `a` заранее зафиксирован как `2`.

## `bind` vs `call`/`apply`

```javascript
fn.call(obj, 1, 2);     // вызывает сразу
fn.apply(obj, [1, 2]);  // вызывает сразу
fn.bind(obj, 1, 2);     // возвращает новую функцию
```

## В обработчиках событий

```javascript
class Counter {
  constructor() {
    this.count = 0;
    this.increment = this.increment.bind(this);
  }

  increment() {
    this.count++;
  }
}
```

Так раньше часто сохраняли контекст метода.

## Подводная деталь

Повторный `bind` не меняет уже привязанный `this`.

```javascript
function showName() {
  return this.name;
}

const fn = showName.bind({ name: "Anna" });
const again = fn.bind({ name: "Max" });

again(); // "Anna"
```

## Мини-шпаргалка

| Метод | Результат |
| --- | --- |
| `fn.call(obj)` | вызов сейчас |
| `fn.apply(obj, args)` | вызов сейчас |
| `fn.bind(obj)` | новая функция |
| `fn.bind(obj, a)` | новая функция с `this` и первым аргументом |
