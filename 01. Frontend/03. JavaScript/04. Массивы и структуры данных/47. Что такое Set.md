# Что такое Set?

> [!NOTE]
> `Set` - коллекция уникальных значений. Если добавить одно и то же значение несколько раз, оно сохранится только один раз.

## Вопрос

Зачем нужен `Set` и чем он отличается от массива?

## Определение

`Set` хранит значения любого типа и автоматически убирает дубликаты. Он сохраняет порядок вставки и дает удобные методы для проверки наличия значения.

## Создание Set

```javascript
const ids = new Set([1, 2, 2, 3]);

console.log(ids);      // Set(3) {1, 2, 3}
console.log(ids.size); // 3
```

## Основные методы

```javascript
const tags = new Set();

tags.add('js');
tags.add('css');
tags.add('js');

console.log(tags.has('js')); // true
console.log(tags.size);      // 2

tags.delete('css');
```

## Удаление дубликатов из массива

```javascript
const numbers = [1, 2, 2, 3, 3, 3];
const uniqueNumbers = [...new Set(numbers)];

console.log(uniqueNumbers); // [1, 2, 3]
```

## Set vs Array

| Ситуация | Лучше подойдет |
| --- | --- |
| Нужен порядок и индексы | `Array` |
| Нужна уникальность | `Set` |
| Часто проверяем наличие | `Set.has()` |
| Нужны `map`, `filter`, `reduce` | `Array` |

## Мини-шпаргалка

```javascript
const set = new Set();

set.add(value);
set.has(value);
set.delete(value);
set.size;
```
