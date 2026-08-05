# Что делает toSpliced()?

> [!NOTE]
> `toSpliced()` возвращает новый массив с удаленными или вставленными элементами, не изменяя исходный массив.

## Вопрос

Как выполнить операцию как у `splice()`, но без мутации массива?

## Определение

`toSpliced(start, deleteCount, ...items)` - немутирующий метод из ES2023. Он создает копию массива, удаляет из нее элементы начиная с индекса `start`, при необходимости вставляет новые элементы и возвращает новый массив.

## Пример

```javascript
const items = ['a', 'b', 'c', 'd'];

const updated = items.toSpliced(1, 2, 'x', 'y');

console.log(updated); // ['a', 'x', 'y', 'd']
console.log(items);   // ['a', 'b', 'c', 'd']
```

## Только удаление

```javascript
const users = ['Ann', 'Bob', 'Max'];

const withoutBob = users.toSpliced(1, 1);

console.log(withoutBob); // ['Ann', 'Max']
```

## Только вставка

```javascript
const numbers = [1, 4];

const result = numbers.toSpliced(1, 0, 2, 3);

console.log(result); // [1, 2, 3, 4]
```

## Сравнение со splice()

```javascript
const arr = [1, 2, 3];

arr.splice(1, 1);

console.log(arr); // [1, 3] - оригинал изменен
```

`splice()` меняет массив, `toSpliced()` возвращает измененную копию.

## Мини-шпаргалка

```javascript
arr.toSpliced(index, count);           // удалить
arr.toSpliced(index, 0, newItem);      // вставить
arr.toSpliced(index, count, newItem);  // заменить
```
