# Что делает instanceof Error?

> [!NOTE] Коротко
> `value instanceof Error` проверяет, находится ли `Error.prototype` в цепочке прототипов значения.

## Вопрос

Как проверить, что пойманное значение является ошибкой?

## Определение

Оператор `instanceof` проверяет связь объекта с классом через цепочку прототипов. Для ошибок его часто используют, чтобы убедиться, что пойманное значение является экземпляром `Error`.

## Пример

```javascript
try {
  throw new Error('Boom');
} catch (error) {
  console.log(error instanceof Error); // true
}
```

## Проверка конкретного типа

```javascript
try {
  JSON.parse('{ broken }');
} catch (error) {
  if (error instanceof SyntaxError) {
    console.log('Invalid JSON');
  }
}
```

Так можно обрабатывать разные типы ошибок по-разному.

## Почему проверка не всегда идеальна

`instanceof` может вести себя неожиданно между разными realm, например iframe, потому что там могут быть свои конструкторы `Error`.

Также в JavaScript можно выбросить не `Error`:

```javascript
throw 'Bad value';
```

Поэтому в надежном коде иногда дополнительно проверяют форму объекта.

## Мини-шпаргалка

```javascript
if (error instanceof Error) {
  console.log(error.message);
}
```
