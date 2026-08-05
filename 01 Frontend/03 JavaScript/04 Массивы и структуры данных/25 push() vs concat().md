# `push()` vs `concat()`

> [!NOTE]
> `push()` мутирует исходный массив и возвращает новую длину. `concat()` не мутирует массив, а возвращает новый массив с добавленными элементами.

## Вопрос

Чем `push()` отличается от `concat()`?

## `push()`

```javascript
const arr = [1, 2];

const result = arr.push(3);

console.log(arr);    // [1, 2, 3]
console.log(result); // 3
```

`push()` меняет исходный массив.

## `concat()`

```javascript
const arr = [1, 2];

const result = arr.concat(3);

console.log(arr);    // [1, 2]
console.log(result); // [1, 2, 3]
```

`concat()` возвращает новый массив.

## Добавление массива

```javascript
const arr = [1, 2];

arr.concat([3, 4]); // [1, 2, 3, 4]
```

`concat` распаковывает массивы на один уровень.

`push` без spread добавит массив как один элемент:

```javascript
const arr = [1, 2];

arr.push([3, 4]);

console.log(arr); // [1, 2, [3, 4]]
```

## Когда что выбирать

Используйте `push`, если мутация допустима.

```javascript
items.push(newItem);
```

Используйте `concat` или spread, если нужен новый массив.

```javascript
const nextItems = items.concat(newItem);
const nextItems2 = [...items, newItem];
```

## Мини-шпаргалка

| Метод | Мутирует | Возвращает |
| --- | --- | --- |
| `push(item)` | да | новую длину |
| `concat(item)` | нет | новый массив |
| `[...arr, item]` | нет | новый массив |
| `push(...items)` | да | новую длину |
| `concat(items)` | нет | новый массив с элементами `items` |
