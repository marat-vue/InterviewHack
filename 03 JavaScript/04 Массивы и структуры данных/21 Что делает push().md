# `push()`

> [!NOTE] Коротко
> `push()` добавляет один или несколько элементов в конец массива, мутирует исходный массив и возвращает новую длину.

## Вопрос

Что делает `push()`?

## Пример

```javascript
const arr = [1, 2];

const length = arr.push(3, 4);

console.log(arr);    // [1, 2, 3, 4]
console.log(length); // 4
```

Важно: `push()` возвращает не массив, а число.

## Мутация

```javascript
const original = [1, 2];
const result = original.push(3);

console.log(original); // [1, 2, 3]
console.log(result);   // 3
```

Если нужно не мутировать массив, используйте spread или `concat`.

```javascript
const next = [...original, 3];
```

## Добавление массива

```javascript
const arr = [1, 2];
const more = [3, 4];

arr.push(more);

console.log(arr); // [1, 2, [3, 4]]
```

Чтобы добавить элементы массива по отдельности:

```javascript
arr.push(...more);
```

## Мини-шпаргалка

| Свойство | `push()` |
| --- | --- |
| добавляет | в конец |
| мутирует | да |
| возвращает | новую длину |
| несколько элементов | да |
| иммутабельная альтернатива | `[...arr, item]`, `concat` |
