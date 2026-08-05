# `splice()`

> [!NOTE]
> `splice()` мутирует массив: может удалять, вставлять и заменять элементы. Возвращает массив удаленных элементов.

## Вопрос

Что делает `splice()`?

## Синтаксис

```javascript
arr.splice(start, deleteCount, ...items);
```

- `start` - индекс начала;
- `deleteCount` - сколько удалить;
- `items` - что вставить.

## Удаление

```javascript
const arr = ["a", "b", "c"];

const removed = arr.splice(1, 1);

console.log(arr);     // ["a", "c"]
console.log(removed); // ["b"]
```

## Вставка

```javascript
const arr = ["a", "c"];

arr.splice(1, 0, "b");

console.log(arr); // ["a", "b", "c"]
```

`deleteCount = 0` значит "ничего не удалять".

## Замена

```javascript
const arr = ["a", "x", "c"];

arr.splice(1, 1, "b");

console.log(arr); // ["a", "b", "c"]
```

## Отрицательный `start`

```javascript
const arr = ["a", "b", "c"];

arr.splice(-1, 1);

console.log(arr); // ["a", "b"]
```

Отрицательный индекс считается с конца.

## Без мутации

Современная альтернатива:

```javascript
const next = arr.toSpliced(1, 1);
```

Или комбинация `slice`:

```javascript
const next = [...arr.slice(0, 1), ...arr.slice(2)];
```

## Мини-шпаргалка

| Задача | Код |
| --- | --- |
| удалить 1 элемент | `arr.splice(index, 1)` |
| вставить | `arr.splice(index, 0, item)` |
| заменить | `arr.splice(index, 1, newItem)` |
| удалить до конца | `arr.splice(index)` |
| без мутации | `arr.toSpliced(...)` |
