# Boxing и Unboxing

> [!NOTE] Коротко
> Boxing временно оборачивает примитив в объектную оболочку, чтобы можно было вызвать метод; unboxing возвращает значение обратно к примитиву.

## Вопрос

Почему у примитивов вроде строки есть методы?

## Определение

В JavaScript примитивы, например `string`, `number`, `boolean`, не являются объектами. Но когда мы обращаемся к методу примитива, движок временно создает объектную оболочку: `String`, `Number` или `Boolean`.

Этот процесс называют boxing. Когда значение снова используется как примитив, происходит unboxing.

## Пример boxing

```javascript
const text = 'hello';

console.log(text.toUpperCase()); // 'HELLO'
```

Строка `text` - примитив, но JavaScript временно оборачивает ее в объект `String`, чтобы вызвать метод.

## Ручная оболочка

```javascript
const primitive = 'hello';
const objectString = new String('hello');

console.log(typeof primitive);    // 'string'
console.log(typeof objectString); // 'object'
```

Создавать такие оболочки вручную почти никогда не нужно.

## Почему new String опасен

```javascript
const value = new Boolean(false);

if (value) {
  console.log('will run');
}
```

Объект всегда truthy, даже если внутри хранит `false`. Это частая ловушка.

## Unboxing

```javascript
const objectNumber = new Number(10);

console.log(objectNumber.valueOf()); // 10
```

`valueOf()` возвращает примитивное значение из объекта-оболочки.

## Практическое правило

Используй примитивы: `'text'`, `123`, `true`. Не создавай `new String`, `new Number`, `new Boolean` без очень специфической причины.

## Мини-шпаргалка

```javascript
'hello'.toUpperCase(); // boxing happens automatically

new String('hello'); // почти всегда не нужно
value.valueOf();     // unboxing
```
