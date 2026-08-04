# Что делает return внутри конструктора?

> [!NOTE] Коротко
> В конструкторе обычно не пишут `return`: при `new` JavaScript сам возвращает созданный экземпляр.

## Вопрос

Что произойдет, если написать `return` внутри конструктора класса?

## Обычное поведение

```javascript
class User {
  constructor(name) {
    this.name = name;
  }
}

const user = new User('Ann');

console.log(user.name); // 'Ann'
```

Конструктор не возвращает значение явно, но результатом `new User()` становится созданный объект.

## return с примитивом

Если вернуть примитив, он будет проигнорирован.

```javascript
class User {
  constructor() {
    this.name = 'Ann';
    return 123;
  }
}

console.log(new User().name); // 'Ann'
```

## return с объектом

Если вернуть объект, он заменит созданный экземпляр.

```javascript
class User {
  constructor() {
    this.name = 'Ann';

    return { name: 'Bob' };
  }
}

const user = new User();

console.log(user.name); // 'Bob'
console.log(user instanceof User); // false
```

Такое поведение почти всегда запутывает код.

## Практическое правило

В конструкторах классов лучше не использовать `return`, кроме очень редких низкоуровневых случаев. Конструктор должен инициализировать `this`, а не подменять объект.

## Мини-шпаргалка

```javascript
constructor() {
  this.value = 1;
  // return обычно не нужен
}
```
