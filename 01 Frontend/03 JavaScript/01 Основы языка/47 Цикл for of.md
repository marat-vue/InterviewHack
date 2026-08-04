# Цикл `for...of`

> [!NOTE] Коротко
> `for...of` перебирает значения iterable-объекта: массива, строки, `Set`, `Map`, NodeList, генератора и других объектов с `Symbol.iterator`.

## Вопрос

Что делает `for...of` и чем отличается от `for`?

## Пример с массивом

```javascript
const numbers = [10, 20, 30];

for (const number of numbers) {
  console.log(number);
}
```

`for...of` сразу дает значение, без ручной работы с индексом.

## Пример со строкой

```javascript
for (const char of "JS") {
  console.log(char);
}
```

Результат:

```text
J
S
```

## `Set` и `Map`

```javascript
const roles = new Set(["admin", "user"]);

for (const role of roles) {
  console.log(role);
}
```

```javascript
const user = new Map([
  ["name", "Anna"],
  ["age", 25],
]);

for (const [key, value] of user) {
  console.log(key, value);
}
```

## Отличие от обычного `for`

Обычный `for` удобен, когда нужен индекс:

```javascript
for (let i = 0; i < items.length; i++) {
  console.log(i, items[i]);
}
```

`for...of` удобен, когда нужен сам элемент:

```javascript
for (const item of items) {
  console.log(item);
}
```

Если нужен индекс с `for...of`:

```javascript
for (const [index, item] of items.entries()) {
  console.log(index, item);
}
```

## Отличие от `for...in`

`for...of` перебирает значения.

```javascript
for (const value of ["a", "b"]) {
  console.log(value); // "a", "b"
}
```

`for...in` перебирает ключи.

```javascript
for (const key in ["a", "b"]) {
  console.log(key); // "0", "1"
}
```

## Мини-шпаргалка

```javascript
for (const value of array) {}
for (const char of string) {}
for (const value of set) {}
for (const [key, value] of map) {}
for (const [i, value] of array.entries()) {}
```
