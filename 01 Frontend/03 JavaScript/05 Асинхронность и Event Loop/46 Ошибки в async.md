# Ошибки в async

> [!NOTE] Коротко
> Ошибки внутри `async`-функции превращаются в rejected Promise, а ошибки из `await` ловятся через `try...catch`.

## Вопрос

Как правильно обрабатывать ошибки в `async`-функциях?

## Ошибка внутри async-функции

```javascript
async function fail() {
  throw new Error('Something went wrong');
}

fail().catch((error) => {
  console.error(error.message);
});
```

`throw` внутри async-функции не выбрасывает ошибку наружу синхронно. Он делает возвращаемый промис отклоненным.

## try...catch с await

```javascript
async function loadUser() {
  try {
    const response = await fetch('/api/user');
    const user = await response.json();

    return user;
  } catch (error) {
    console.error('Failed to load user:', error);
    throw error;
  }
}
```

`try...catch` поймает ошибку из отклоненного промиса, который стоит после `await`.

## Проверка HTTP-ошибок

`fetch` отклоняется при сетевой ошибке, но не отклоняется автоматически при HTTP-статусах вроде `404` или `500`.

```javascript
async function loadData() {
  const response = await fetch('/api/data');

  if (!response.ok) {
    throw new Error(`HTTP error: ${response.status}`);
  }

  return response.json();
}
```

## Необработанный rejected Promise

```javascript
async function run() {
  await Promise.reject(new Error('Boom'));
}

run(); // ошибка не обработана здесь
```

Лучше:

```javascript
run().catch(console.error);
```

или:

```javascript
try {
  await run();
} catch (error) {
  console.error(error);
}
```

## Ошибки в параллельных запросах

```javascript
try {
  const [user, posts] = await Promise.all([
    loadUser(),
    loadPosts(),
  ]);
} catch (error) {
  console.error('At least one request failed', error);
}
```

`Promise.all()` упадет при первой ошибке.

## Мини-шпаргалка

```javascript
try {
  const data = await task();
} catch (error) {
  handleError(error);
}
```
