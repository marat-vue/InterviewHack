# Что делает SharedWorker?

> [!NOTE] Коротко
> `SharedWorker` позволяет нескольким вкладкам или окнам одного origin подключаться к одному общему worker-потоку.

## Вопрос

Чем `SharedWorker` отличается от обычного `Web Worker`?

## Определение

`SharedWorker` - разновидность worker, к которому могут подключиться несколько контекстов: вкладки, окна, iframe одного origin. Он живет отдельно от конкретной страницы и может координировать общие данные между ними.

Обычный `Worker` обычно принадлежит одной странице. `SharedWorker` может быть общим.

## Создание SharedWorker

```javascript
const worker = new SharedWorker('shared-worker.js');

worker.port.start();
worker.port.postMessage({ type: 'PING' });

worker.port.onmessage = (event) => {
  console.log(event.data);
};
```

Обмен идет через `worker.port`.

## shared-worker.js

```javascript
const ports = [];

self.onconnect = (event) => {
  const port = event.ports[0];
  ports.push(port);

  port.onmessage = (messageEvent) => {
    port.postMessage({
      type: 'PONG',
      payload: messageEvent.data,
    });
  };

  port.start();
};
```

Каждое новое подключение приходит через событие `connect`.

## Где применять

- общий кэш между вкладками;
- синхронизация состояния;
- один WebSocket на несколько вкладок;
- координация фоновой логики внутри одного origin.

## Ограничения

- нет доступа к DOM;
- работает в рамках одного origin;
- поддержка и поведение могут отличаться между окружениями;
- чаще используется реже, чем обычный `Worker` или `Service Worker`.

## Мини-шпаргалка

```javascript
const shared = new SharedWorker('worker.js');

shared.port.start();
shared.port.postMessage(data);
shared.port.onmessage = (event) => {};
```
