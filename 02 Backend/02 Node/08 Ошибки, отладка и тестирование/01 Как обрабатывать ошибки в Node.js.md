# Как обрабатывать ошибки в Node.js?

> [!NOTE]
> Ошибки в Node.js обрабатывают по-разному в зависимости от стиля кода: `try/catch` для `async/await`, `.catch()` для Promise, первый аргумент callback для callback API и middleware ошибок во фреймворках.

## Синхронные ошибки

```js
try {
  const data = JSON.parse('{ bad json }');
  console.log(data);
} catch (error) {
  console.error('JSON не распарсился:', error.message);
}
```

## Ошибки в async/await

```js
import { readFile } from 'node:fs/promises';

try {
  const text = await readFile('missing.txt', 'utf8');
  console.log(text);
} catch (error) {
  console.error('Файл не прочитан:', error.message);
}
```

## Ошибки в Promise

```js
readFile('missing.txt', 'utf8')
  .then(console.log)
  .catch((error) => {
    console.error(error.message);
  });
```

## Ошибки в HTTP-сервере

В обработчике запроса нельзя отправлять пользователю внутренние детали ошибки.

```js
try {
  const user = await getUser();
  res.end(JSON.stringify(user));
} catch (error) {
  console.error(error);
  res.statusCode = 500;
  res.end(JSON.stringify({ message: 'Internal server error' }));
}
```

## Мини-шпаргалка

- `throw` создает исключение.
- `try/catch` ловит sync ошибки и ошибки из `await`.
- Promise-ошибки ловятся через `.catch()`.
- В HTTP не раскрывай пользователю stack trace.
- Ошибки нужно логировать с контекстом.
