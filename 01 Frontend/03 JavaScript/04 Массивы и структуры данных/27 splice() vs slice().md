# `splice()` vs `slice()`

> [!NOTE] Коротко
> `splice()` меняет исходный массив и возвращает удаленные элементы. `slice()` не меняет исходный массив и возвращает копию выбранной части.

## Вопрос

Чем `splice()` отличается от `slice()`?

## `splice`

```javascript
const arr = ["a", "b", "c"];

const removed = arr.splice(1, 1);

console.log(arr);     // ["a", "c"]
console.log(removed); // ["b"]
```

Используется для удаления, вставки и замены.

## `slice`

```javascript
const arr = ["a", "b", "c"];

const part = arr.slice(1, 3);

console.log(arr);  // ["a", "b", "c"]
console.log(part); // ["b", "c"]
```

`slice(start, end)` берет элементы от `start` до `end`, не включая `end`.

## Копия массива

```javascript
const copy = arr.slice();
```

Это поверхностная копия.

## Отрицательные индексы

```javascript
const arr = ["a", "b", "c"];

arr.slice(-2); // ["b", "c"]
```

`splice` тоже поддерживает отрицательный `start`, но мутирует массив.

## Мини-шпаргалка

| Метод | Мутирует | Возвращает | Использование |
| --- | --- | --- | --- |
| `splice` | да | удаленные элементы | удалить/вставить/заменить |
| `slice` | нет | копию части | получить фрагмент |
| `slice()` | нет | поверхностную копию | копирование |
| `toSpliced` | нет | новый массив | иммутабельный splice |
