# Что делает ключевое слово async?

> [!NOTE]
> `async` объявляет функцию асинхронной: она всегда возвращает `Promise` и позволяет использовать внутри `await`.

## Вопрос

Что меняется, когда перед функцией стоит `async`?

## Определение

Ключевое слово `async` ставится перед объявлением функции, function expression или стрелочной функцией. Такая функция всегда возвращает промис.

Если внутри вернуть обычное значение, JavaScript автоматически обернет его в `Promise.resolve(value)`. Если внутри бросить ошибку, функция вернет отклоненный промис.

## Пример с обычным значением

```javascript
async function getName() {
  return 'Ann';
}

getName().then(console.log); // 'Ann'
```

Фактически результат похож на:

```javascript
function getName() {
  return Promise.resolve('Ann');
}
```

## Пример с ошибкой

```javascript
async function fail() {
  throw new Error('Broken');
}

fail().catch((error) => {
  console.error(error.message); // 'Broken'
});
```

Ошибка внутри async-функции превращается в rejected Promise.

## async нужен для await

```javascript
async function loadUser() {
  const response = await fetch('/api/user');

  return response.json();
}
```

`await` можно использовать внутри `async`-функции. В современных ES-модулях также доступен top-level `await`.

## Мини-шпаргалка

```javascript
async function fn() {
  return value; // Promise.resolve(value)
}
```
