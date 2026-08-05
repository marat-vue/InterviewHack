# Что возвращает async-функция?

> [!NOTE]
> Async-функция всегда возвращает `Promise`, даже если внутри написан обычный `return`.

## Вопрос

Что вернет функция, объявленная с `async`?

## Определение

Любая `async`-функция возвращает промис. Возвращаемое значение становится успешным результатом этого промиса. Исключение становится причиной отклонения.

## Обычный return

```javascript
async function getNumber() {
  return 42;
}

const result = getNumber();

console.log(result); // Promise

const value = await result;
console.log(value); // 42
```

## Возврат промиса

```javascript
async function loadData() {
  return fetch('/api/data');
}
```

Если `async`-функция возвращает промис, внешний промис дождется его результата.

## Ошибка внутри async-функции

```javascript
async function fail() {
  throw new Error('Nope');
}

try {
  await fail();
} catch (error) {
  console.error(error.message); // 'Nope'
}
```

## Частая ошибка

```javascript
async function getUser() {
  return { name: 'Ann' };
}

const user = getUser();

console.log(user.name); // undefined
```

`user` здесь промис, а не объект. Нужно использовать `await` или `.then()`.

## Мини-шпаргалка

```javascript
async function fn() {
  return 1;
}

await fn(); // 1
```
