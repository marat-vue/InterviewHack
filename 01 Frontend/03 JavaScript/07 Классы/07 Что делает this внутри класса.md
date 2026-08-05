# Что делает this внутри класса?

> [!NOTE]
> `this` внутри класса обычно указывает на конкретный экземпляр, созданный через `new`.

## Вопрос

Что означает `this` в конструкторе и методах класса?

## this в constructor

```javascript
class User {
  constructor(name) {
    this.name = name;
  }
}

const user = new User('Ann');

console.log(user.name); // 'Ann'
```

В конструкторе `this` - новый объект, который создается через `new`.

## this в методе

```javascript
class User {
  constructor(name) {
    this.name = name;
  }

  sayHi() {
    return `Hi, ${this.name}`;
  }
}
```

При вызове `user.sayHi()` значение `this` будет равно `user`.

## Потеря this

```javascript
const user = new User('Ann');
const sayHi = user.sayHi;

sayHi(); // TypeError или undefined внутри this
```

Метод потерял объект слева от точки, поэтому `this` больше не указывает на `user`.

## Как исправить

```javascript
const boundSayHi = user.sayHi.bind(user);

boundSayHi();
```

Или использовать стрелочное поле класса, если метод часто передается как callback.

## Мини-шпаргалка

```javascript
object.method(); // this === object
const fn = object.method;
fn(); // this потерян
```
