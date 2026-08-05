# `Array.from()`

> [!NOTE]
> `Array.from()` создает новый массив из iterable или array-like объекта. Также может сразу применить mapping-функцию.

## Вопрос

Что делает `Array.from()`?

## Синтаксис

```javascript
Array.from(source, mapFn);
```

## Из строки

```javascript
Array.from("hello");
// ["h", "e", "l", "l", "o"]
```

## Из Set

```javascript
const set = new Set([1, 2, 2, 3]);

Array.from(set); // [1, 2, 3]
```

## Из псевдомассива

```javascript
function demo() {
  const args = Array.from(arguments);

  return args.map((value) => value * 2);
}

demo(1, 2, 3); // [2, 4, 6]
```

## С mapping-функцией

```javascript
Array.from([1, 2, 3], (number) => number * 2);
// [2, 4, 6]
```

Это похоже на:

```javascript
Array.from(source).map(mapFn);
```

но делает преобразование сразу.

## Создание диапазона

```javascript
Array.from({ length: 5 }, (_, index) => index + 1);
// [1, 2, 3, 4, 5]
```

## Мини-шпаргалка

| Источник | Пример |
| --- | --- |
| string | `Array.from("abc")` |
| Set | `Array.from(set)` |
| NodeList | `Array.from(nodes)` |
| arguments | `Array.from(arguments)` |
| array-like | `Array.from({ length: 3 })` |
| с map | `Array.from(arr, fn)` |
