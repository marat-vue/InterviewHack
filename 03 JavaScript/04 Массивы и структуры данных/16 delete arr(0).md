# `delete arr[0]`

> [!NOTE] Коротко
> `delete arr[index]` удаляет свойство с индексом, но не сдвигает элементы и не меняет `length`. В массиве появляется пустой слот.

## Вопрос

Что произойдет при `delete arr[0]`?

## Пример

```javascript
const numbers = [10, 20, 30];

delete numbers[0];

console.log(numbers);        // [empty, 20, 30]
console.log(numbers.length); // 3
```

Элемент удален, но длина осталась прежней.

## Почему так

Массив - объект, а индекс - свойство.

```javascript
delete numbers[0];
```

Оператор `delete` удаляет свойство, а не выполняет "нормальное удаление элемента массива".

## Empty slot

```javascript
0 in numbers; // false
numbers[0];   // undefined
```

`undefined` при чтении не означает, что там лежит значение `undefined`. Это может быть пустой слот.

## Что использовать вместо

Если нужно удалить элемент со сдвигом:

```javascript
numbers.splice(0, 1);
```

Если нужно получить новый массив без элемента:

```javascript
const withoutFirst = numbers.slice(1);
```

или:

```javascript
const result = numbers.filter((_, index) => index !== 0);
```

## Мини-шпаргалка

| Операция | Что делает |
| --- | --- |
| `delete arr[i]` | создает empty slot |
| `arr.splice(i, 1)` | удаляет со сдвигом |
| `arr.length` после delete | не меняется |
| `i in arr` после delete | `false` |
