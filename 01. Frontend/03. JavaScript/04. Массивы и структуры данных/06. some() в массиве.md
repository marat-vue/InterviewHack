# `some()` в массиве

> [!NOTE]
> `some()` проверяет, есть ли в массиве хотя бы один элемент, удовлетворяющий условию. Возвращает boolean и останавливается на первом `true`.

## Вопрос

Для чего используется `arr.some()`? Чем отличается от `every()`?

## Синтаксис

```javascript
const result = array.some((element, index, array) => {
  return condition;
});
```

## Пример

```javascript
const numbers = [1, 2, 3, 4];

numbers.some((number) => number > 3); // true
numbers.some((number) => number > 10); // false
```

## Останавливается рано

```javascript
const hasAdmin = users.some((user) => user.role === "admin");
```

Как только найден первый `admin`, дальнейший обход не нужен.

## Пустой массив

```javascript
[].some((item) => true); // false
```

В пустом массиве нет элемента, который удовлетворяет условию.

## `some` vs `every`

```javascript
numbers.some((n) => n > 0);  // хотя бы один
numbers.every((n) => n > 0); // все
```

## Мини-шпаргалка

| Метод | Вопрос | Пустой массив |
| --- | --- | --- |
| `some` | есть хотя бы один? | `false` |
| `every` | все подходят? | `true` |
| `find` | какой первый подходит? | `undefined` |
