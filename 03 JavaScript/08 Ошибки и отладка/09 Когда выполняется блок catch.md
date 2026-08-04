# Когда выполняется блок catch?

> [!NOTE] Коротко
> Блок `catch` выполняется только если внутри соответствующего `try` было выброшено исключение.

## Вопрос

Когда JavaScript переходит в `catch`?

## Определение

`catch` запускается, если в блоке `try` возникла ошибка или был выполнен оператор `throw`. Если ошибок нет, `catch` пропускается.

## Пример с ошибкой

```javascript
try {
  throw new Error('Failed');
} catch (error) {
  console.log(error.message); // 'Failed'
}
```

## Пример без ошибки

```javascript
try {
  console.log('ok');
} catch (error) {
  console.log('will not run');
}
```

`catch` не выполнится.

## Ошибка внутри вызванной функции

```javascript
function parseJson(text) {
  return JSON.parse(text);
}

try {
  parseJson('{ broken }');
} catch (error) {
  console.log(error.name); // 'SyntaxError'
}
```

`catch` ловит ошибку, даже если она возникла в функции, вызванной внутри `try`.

## catch без параметра

```javascript
try {
  riskyCode();
} catch {
  console.log('Something went wrong');
}
```

Если объект ошибки не нужен, параметр можно не указывать.

## Мини-шпаргалка

```javascript
try {
  // if throw happens here
} catch (error) {
  // catch runs here
}
```
