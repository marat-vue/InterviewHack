# Когда использовать cluster?

> [!NOTE]
> `cluster` позволяет запустить несколько Node.js-процессов, которые могут разделять один серверный порт. Это способ использовать несколько CPU-ядер для HTTP-сервера внутри одной машины.

## Зачем cluster?

Один Node.js-процесс обычно выполняет JavaScript в одном основном потоке. Если сервер запущен на машине с несколькими ядрами, один процесс не использует их полностью.

`cluster` запускает primary process и worker processes.

```txt
primary
  worker 1 -> HTTP server
  worker 2 -> HTTP server
  worker 3 -> HTTP server
```

## Пример

```js
import cluster from 'node:cluster';
import http from 'node:http';
import { availableParallelism } from 'node:os';
import process from 'node:process';

if (cluster.isPrimary) {
  for (let i = 0; i < availableParallelism(); i += 1) {
    cluster.fork();
  }
} else {
  http.createServer((req, res) => {
    res.end(`worker ${process.pid}`);
  }).listen(3000);
}
```

## cluster vs worker_threads

| Инструмент | Изоляция | Подходит для |
|---|---|---|
| `cluster` | отдельные процессы | масштабирование HTTP-сервера |
| `worker_threads` | потоки в процессе | CPU-bound вычисления |

## Мини-шпаргалка

- `cluster` масштабирует Node.js по процессам.
- Workers могут слушать один порт.
- Память между процессами не общая.
- Упавший worker можно перезапустить.
- В контейнерах часто масштабируют не через cluster, а количеством replicas.
