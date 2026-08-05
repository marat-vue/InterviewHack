# Как работает IPC между процессами?

> [!NOTE]
> IPC, или inter-process communication, - обмен сообщениями между процессами. В Node.js он доступен для forked child processes и cluster workers через `send` и событие `message`.

## child_process.fork

`fork` запускает другой Node.js-файл и создает канал сообщений.

```js
import { fork } from 'node:child_process';

const child = fork('./worker.js');

child.send({ type: 'sum', values: [1, 2, 3] });

child.on('message', (message) => {
  console.log('Ответ:', message);
});
```

Файл worker:

```js
process.on('message', (message) => {
  if (message.type === 'sum') {
    const result = message.values.reduce((sum, value) => sum + value, 0);
    process.send({ result });
  }
});
```

## Что можно передавать?

Обычно передают сериализуемые сообщения: объекты, строки, числа. Для некоторых handle-объектов Node.js поддерживает специальные сценарии передачи.

## IPC vs HTTP

IPC удобен для процессов внутри одной машины и одного приложения. Для связи между сервисами чаще используют HTTP, gRPC, очереди или брокеры сообщений.

## Мини-шпаргалка

- IPC - обмен сообщениями между процессами.
- `child_process.fork` создает IPC-канал.
- `process.send` отправляет сообщение родителю.
- Сообщения лучше делать явными: `{ type, payload }`.
- Для межсервисного общения IPC обычно не подходит.
