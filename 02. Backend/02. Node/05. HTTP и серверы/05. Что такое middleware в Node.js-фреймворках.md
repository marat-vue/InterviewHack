# Что такое middleware в Node.js-фреймворках?

> [!NOTE]
> Middleware - это промежуточная функция, которая выполняется между получением запроса и отправкой ответа. Она может логировать запрос, проверять авторизацию, парсить body, добавлять данные в `req` или завершать ответ.

## Идея middleware

В веб-фреймворках запрос проходит через цепочку функций.

```js
request -> middleware -> middleware -> route handler -> response
```

Каждая middleware может:

- пропустить запрос дальше;
- изменить `req` или `res`;
- завершить ответ;
- передать ошибку в обработчик ошибок.

## Пример на Express

```js
import express from 'express';

const app = express();

app.use((req, res, next) => {
  console.log(req.method, req.url);
  next();
});

app.get('/profile', (req, res) => {
  res.json({ name: 'Анна' });
});

app.listen(3000);
```

`next()` передает управление следующей middleware или маршруту.

## Middleware авторизации

```js
function requireAuth(req, res, next) {
  const token = req.headers.authorization;

  if (!token) {
    res.status(401).json({ message: 'Token required' });
    return;
  }

  next();
}

app.get('/admin', requireAuth, (req, res) => {
  res.json({ ok: true });
});
```

## Ошибочная middleware

В Express middleware обработки ошибок имеет четыре аргумента:

```js
app.use((error, req, res, next) => {
  console.error(error);
  res.status(500).json({ message: 'Internal server error' });
});
```

## Мини-шпаргалка

- Middleware - функция между запросом и ответом.
- `next()` передает управление дальше.
- Middleware удобны для логов, авторизации, CORS, body parsing.
- Middleware может завершить ответ сама.
- Порядок регистрации middleware важен.
