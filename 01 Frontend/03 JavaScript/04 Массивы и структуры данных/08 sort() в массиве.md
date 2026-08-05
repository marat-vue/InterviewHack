# `sort()` в массиве

> [!NOTE]
> `sort()` сортирует массив на месте и возвращает тот же массив. По умолчанию элементы сравниваются как строки, поэтому для чисел почти всегда нужен `compareFn`.

## Вопрос

Какие задачи решает `arr.sort()`? Какие аргументы принимает и почему часто лучше писать `[...arr].sort()`?

## Базовый пример

```javascript
const names = ["Max", "Anna", "Kate"];

names.sort();

console.log(names); // ["Anna", "Kate", "Max"]
```

`sort` мутирует исходный массив.

## Ловушка с числами

```javascript
[10, 2, 30].sort(); // [10, 2, 30]
```

По умолчанию сортировка идет как строковая:

```javascript
"10" < "2"; // true
```

Для чисел:

```javascript
const numbers = [10, 2, 30];

numbers.sort((a, b) => a - b); // [2, 10, 30]
```

По убыванию:

```javascript
numbers.sort((a, b) => b - a);
```

## Сортировка без мутации

```javascript
const sorted = [...numbers].sort((a, b) => a - b);
```

Или современный метод:

```javascript
const sorted = numbers.toSorted((a, b) => a - b);
```

## Сортировка объектов

```javascript
const users = [
  { name: "Anna", age: 25 },
  { name: "Max", age: 20 },
];

users.sort((a, b) => a.age - b.age);
```

Для строк:

```javascript
users.sort((a, b) => a.name.localeCompare(b.name));
```

## Мини-шпаргалка

| Задача | Код |
| --- | --- |
| числа по возрастанию | `arr.sort((a, b) => a - b)` |
| числа по убыванию | `arr.sort((a, b) => b - a)` |
| строки | `arr.sort()` или `localeCompare` |
| без мутации | `[...arr].sort()` |
| современно без мутации | `arr.toSorted()` |
