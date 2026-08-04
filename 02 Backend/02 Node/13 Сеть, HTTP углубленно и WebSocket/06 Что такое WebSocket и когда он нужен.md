# Что такое WebSocket и когда он нужен?

> [!NOTE]
> WebSocket - протокол для постоянного двустороннего соединения между клиентом и сервером. Он нужен, когда сервер должен отправлять данные клиенту сразу, без постоянного polling.

## Когда нужен WebSocket?

WebSocket подходит для:

- чатов;
- real-time уведомлений;
- совместного редактирования;
- онлайн-игр;
- live dashboards;
- торговых терминалов;
- статусов долгих операций.

## WebSocket client в Node.js

В современных версиях Node.js есть встроенный WebSocket client.

```js
const socket = new WebSocket('wss://example.com/socket');

socket.addEventListener('open', () => {
  socket.send(JSON.stringify({ type: 'ping' }));
});

socket.addEventListener('message', (event) => {
  console.log(event.data);
});
```

## WebSocket server

Для сервера обычно используют библиотеку, например `ws`, Socket.IO или возможности выбранного фреймворка.

```js
import { WebSocketServer } from 'ws';

const wss = new WebSocketServer({ port: 8080 });

wss.on('connection', (socket) => {
  socket.send('connected');

  socket.on('message', (message) => {
    socket.send(`echo: ${message}`);
  });
});
```

## WebSocket vs HTTP polling vs SSE

| Подход | Когда выбирать |
|---|---|
| Polling | редко обновляемые данные, простота |
| SSE | сервер отправляет события клиенту, клиент только слушает |
| WebSocket | двусторонний real-time обмен |

## Мини-шпаргалка

- WebSocket держит постоянное соединение.
- Подходит для двустороннего real-time.
- В Node.js есть встроенный WebSocket client.
- WebSocket server обычно делают через библиотеку.
- Для однонаправленных событий иногда проще SSE.
