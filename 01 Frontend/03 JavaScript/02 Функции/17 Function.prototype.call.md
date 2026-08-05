# `Function.prototype.call`

> [!NOTE]
> `call()` сразу вызывает функцию и явно задает значение `this`. Аргументы передаются через запятую.

## Вопрос

Что делает `Function.prototype.call`?

## Синтаксис

```javascript
fn.call(thisArg, arg1, arg2, ...);
```

`thisArg` станет значением `this` внутри функции.

## Пример

```javascript
function sayHi() {
  return `Hi, ${this.name}`;
}

const user = { name: "Anna" };

sayHi.call(user); // "Hi, Anna"
```

## Передача аргументов

```javascript
function introduce(role, city) {
  return `${this.name}, ${role}, ${city}`;
}

const user = { name: "Anna" };

introduce.call(user, "developer", "Moscow");
// "Anna, developer, Moscow"
```

Аргументы идут после `thisArg` обычным списком.

## Заимствование метода

```javascript
const user = {
  name: "Anna",
};

function printName() {
  return this.name;
}

printName.call(user); // "Anna"
```

Функция не принадлежит объекту, но ее можно вызвать с этим объектом как `this`.

## `call` vs обычный вызов

```javascript
printName();       // this зависит от режима и окружения
printName.call(user); // this явно равен user
```

## Мини-шпаргалка

| Метод | Что делает |
| --- | --- |
| `fn.call(obj, a, b)` | вызывает `fn`, `this = obj`, аргументы списком |
| `fn.apply(obj, [a, b])` | вызывает `fn`, аргументы массивом |
| `fn.bind(obj)` | не вызывает, возвращает новую функцию |
