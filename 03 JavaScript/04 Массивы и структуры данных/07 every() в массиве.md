# `every()` в массиве

> [!NOTE] Коротко
> `every()` проверяет, что все элементы массива удовлетворяют условию. Возвращает boolean и останавливается на первом `false`.

## Вопрос

Когда используется `arr.every()` и чем отличается от `some()`?

## Синтаксис

```javascript
const result = array.every((element, index, array) => {
  return condition;
});
```

## Пример

```javascript
const numbers = [2, 4, 6];

numbers.every((number) => number % 2 === 0); // true
numbers.every((number) => number > 3);       // false
```

## Останавливается рано

Если callback вернул `false`, дальнейший обход прекращается.

```javascript
const allValid = fields.every((field) => field.isValid);
```

## Пустой массив

```javascript
[].every((item) => false); // true
```

Это называют vacuous truth: в пустом массиве нет элемента, который нарушает условие.

## `every` vs `some`

```javascript
users.every((user) => user.active); // все активны?
users.some((user) => user.active);  // есть хотя бы один активный?
```

## Мини-шпаргалка

| Метод | Смысл | Остановка |
| --- | --- | --- |
| `every` | все элементы подходят | на первом `false` |
| `some` | хотя бы один подходит | на первом `true` |
| `filter` | собрать все подходящие | проходит весь массив |
