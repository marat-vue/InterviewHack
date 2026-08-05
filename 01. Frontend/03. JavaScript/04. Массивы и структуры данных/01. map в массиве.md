# `map()` в массиве

> [!NOTE]
> `map()` создает новый массив, применяя callback к каждому элементу. Исходный массив не изменяется, а длина результата обычно такая же, как у исходного массива.

## Вопрос

Для чего используется `map()`? Какие есть особенности?

## Синтаксис

```javascript
const result = array.map((element, index, array) => {
  return newValue;
});
```

## Пример

```javascript
const numbers = [1, 2, 3];

const doubled = numbers.map((number) => number * 2);

console.log(doubled); // [2, 4, 6]
console.log(numbers); // [1, 2, 3]
```

## Когда использовать

`map` нужен, когда нужно преобразовать каждый элемент.

```javascript
const users = [
  { id: 1, name: "Anna" },
  { id: 2, name: "Max" },
];

const names = users.map((user) => user.name);
// ["Anna", "Max"]
```

## Важно вернуть значение

```javascript
const result = [1, 2, 3].map((number) => {
  number * 2;
});

console.log(result); // [undefined, undefined, undefined]
```

С фигурными скобками нужен `return`.

```javascript
const result = [1, 2, 3].map((number) => {
  return number * 2;
});
```

## `map` не для side effects

Если результат не нужен, лучше `forEach`.

```javascript
users.map((user) => console.log(user.name)); // плохой стиль
users.forEach((user) => console.log(user.name)); // лучше
```

## Мини-шпаргалка

| Свойство | `map()` |
| --- | --- |
| возвращает | новый массив |
| мутирует исходный | нет |
| задача | преобразование |
| длина результата | обычно такая же |
| callback | `(element, index, array)` |
