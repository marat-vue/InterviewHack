# `this` внутри метода объекта

> [!NOTE]
> В методе объекта `this` определяется способом вызова. При вызове `obj.method()` значение `this` обычно равно `obj`.

## Вопрос

Как работает `this` внутри метода объекта?

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

## Не место объявления, а способ вызова

```javascript
function sayHi() {
  return `Hi, ${this.name}`;
}

const user = { name: "Anna", sayHi };
const admin = { name: "Max", sayHi };

user.sayHi();  // "Hi, Anna"
admin.sayHi(); // "Hi, Max"
```

Функция одна, но `this` разный.

## Потеря контекста

```javascript
const fn = user.sayHi;

fn(); // this потерян
```

Функция больше не вызывается через `user`.

Исправление:

```javascript
const fn = user.sayHi.bind(user);

fn(); // "Hi, Anna"
```

## Стрелочная функция как метод

```javascript
const user = {
  name: "Anna",
  sayHi: () => `Hi, ${this.name}`,
};
```

Стрелочная функция не имеет собственного `this`, поэтому такой метод обычно не работает как ожидается.

## Вложенная функция

```javascript
const user = {
  name: "Anna",
  sayHi() {
    function inner() {
      return this.name;
    }

    return inner();
  },
};
```

У `inner` свой `this`, и он не равен `user`. Часто используют стрелку:

```javascript
const user = {
  name: "Anna",
  sayHi() {
    const inner = () => this.name;

    return inner();
  },
};
```

## Мини-шпаргалка

| Вызов | `this` |
| --- | --- |
| `obj.method()` | `obj` |
| `const fn = obj.method; fn()` | контекст потерян |
| `fn.call(obj)` | `obj` |
| `fn.bind(obj)` | закрепленный `obj` |
| arrow method | внешний `this`, не объект |
