# Ключевое слово `arguments`

> [!NOTE] Коротко
> `arguments` - псевдомассив со всеми аргументами обычной функции. У стрелочных функций своего `arguments` нет; в современном коде чаще используют rest-параметры `...args`.

## Вопрос

Что делает ключевое слово `arguments`? Какие особенности использования со стрелочной функцией?

## Что такое `arguments`

```javascript
function showArgs() {
  console.log(arguments);
  console.log(arguments.length);
}

showArgs("a", "b", "c");
```

`arguments` содержит все переданные аргументы, даже если они не описаны в параметрах.

```javascript
function sum() {
  let total = 0;

  for (const value of arguments) {
    total += value;
  }

  return total;
}

sum(1, 2, 3); // 6
```

## Псевдомассив

`arguments` похож на массив:

```javascript
arguments[0];
arguments.length;
```

Но это не настоящий массив:

```javascript
arguments.map; // undefined
```

Можно преобразовать:

```javascript
const args = Array.from(arguments);
```

или:

```javascript
const args = [...arguments];
```

## У стрелочных функций нет `arguments`

```javascript
const showArgs = () => {
  console.log(arguments); // возьмет из внешней области или даст ошибку
};
```

Используйте rest-параметры:

```javascript
const showArgs = (...args) => {
  console.log(args);
};
```

## `arguments` vs rest

```javascript
function oldStyle() {
  console.log(arguments);
}

function modernStyle(...args) {
  console.log(args);
}
```

`args` - настоящий массив, поэтому можно сразу использовать `map`, `filter`, `reduce`.

## Мини-шпаргалка

| Свойство | `arguments` | `...args` |
| --- | --- | --- |
| Где работает | обычные функции | любые функции |
| Тип | псевдомассив | настоящий массив |
| Методы массива | нет | есть |
| Стрелочные функции | своего нет | работает |
| Современный выбор | редко | обычно да |
