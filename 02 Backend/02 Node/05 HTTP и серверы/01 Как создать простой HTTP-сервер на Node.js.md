# Как создать простой HTTP-сервер на Node.js?

> [!NOTE]
> HTTP-сервер в Node.js можно создать без фреймворков через встроенный модуль `node:http`. Он принимает запросы, формирует ответы и дает понять, как работают Express, Fastify и другие серверные фреймворки.

## Минимальный сервер

```js
import http from 'node:http';

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain; charset=utf-8');
  res.end('Привет из Node.js');
});

server.listen(3000, () => {
  console.log('Сервер запущен: http://localhost:3000');
});
```

`createServer` принимает функцию-обработчик. Она вызывается на каждый HTTP-запрос.

## Что происходит внутри?

1. Клиент отправляет HTTP-запрос.
2. Node.js создает объекты `req` и `res`.
3. Твой обработчик читает запрос.
4. Твой код записывает статус, заголовки и тело ответа.
5. `res.end()` завершает ответ.

## Пример маршрутизации без Express

```js
import http from 'node:http';

http.createServer((req, res) => {
  if (req.method === 'GET' && req.url === '/health') {
    res.writeHead(200, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({ ok: true }));
    return;
  }

  res.writeHead(404, { 'Content-Type': 'text/plain; charset=utf-8' });
  res.end('Не найдено');
}).listen(3000);
```

## Мини-шпаргалка

- `node:http` позволяет поднять сервер без зависимостей.
- `req` описывает входящий запрос.
- `res` используется для отправки ответа.
- `res.end()` обязателен для завершения ответа.
- Низкоуровневый HTTP полезно понимать даже при работе с Express.
