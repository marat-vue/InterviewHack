# `pop()`

> [!NOTE] Коротко
> `pop()` удаляет последний элемент массива, мутирует исходный массив и возвращает удаленный элемент. Если массив пустой, возвращает `undefined`.

## Вопрос

Что делает `pop()`?

## Пример

```javascript
const arr = [1, 2, 3];

const removed = arr.pop();

console.log(removed); // 3
console.log(arr);     // [1, 2]
```

## Пустой массив

```javascript
const arr = [];

arr.pop(); // undefined
```

Ошибки не будет.

## Мутация

`pop()` меняет исходный массив.

```javascript
const arr = ["a", "b"];
const sameArray = arr;

arr.pop();

console.log(sameArray); // ["a"]
```

## Без мутации

Получить последний элемент без удаления:

```javascript
const last = arr.at(-1);
```

Получить массив без последнего элемента:

```javascript
const withoutLast = arr.slice(0, -1);
```

## Мини-шпаргалка

| Задача | Код |
| --- | --- |
| удалить последний | `arr.pop()` |
| получить последний без удаления | `arr.at(-1)` |
| копия без последнего | `arr.slice(0, -1)` |
| пустой массив | `pop()` вернет `undefined` |
