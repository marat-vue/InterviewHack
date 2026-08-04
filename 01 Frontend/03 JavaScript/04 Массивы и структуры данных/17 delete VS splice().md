# `delete` vs `splice()`

> [!NOTE] Коротко
> `delete arr[i]` удаляет свойство и оставляет пустой слот. `splice(i, 1)` удаляет элемент массива, сдвигает остальные элементы и меняет `length`.

## Вопрос

Чем `delete` отличается от `splice()` при удалении элемента массива?

## `delete`

```javascript
const arr = ["a", "b", "c"];

delete arr[1];

console.log(arr);        // ["a", empty, "c"]
console.log(arr.length); // 3
```

`delete` не сдвигает элементы.

```javascript
1 in arr; // false
```

## `splice`

```javascript
const arr = ["a", "b", "c"];

arr.splice(1, 1);

console.log(arr);        // ["a", "c"]
console.log(arr.length); // 2
```

`splice` удаляет элемент как элемент массива.

## Возвращаемое значение `splice`

```javascript
const arr = ["a", "b", "c"];
const removed = arr.splice(1, 1);

console.log(removed); // ["b"]
```

`splice` возвращает массив удаленных элементов.

## Мутация

Оба варианта мутируют массив, но по-разному.

Если нужен новый массив без мутации:

```javascript
const result = arr.filter((_, index) => index !== 1);
```

Или современный вариант:

```javascript
const result = arr.toSpliced(1, 1);
```

## Мини-шпаргалка

| Операция | `delete` | `splice` |
| --- | --- | --- |
| меняет `length` | нет | да |
| сдвигает элементы | нет | да |
| оставляет empty slot | да | нет |
| возвращает удаленное | boolean-like результат оператора | массив удаленных |
| использовать для массивов | редко | часто |
