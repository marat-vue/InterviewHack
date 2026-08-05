# Что такое libuv и thread pool в Node.js

> [!NOTE]
> **libuv** - низкоуровневая библиотека, на которой Node.js строит event loop, timers, async I/O и thread pool. Thread pool помогает выполнять некоторые операции, которые не могут быть полностью неблокирующими на уровне ОС.

## Главное

Node.js не выполняет всю работу только в одном JS-потоке.

```text
JavaScript thread
  -> libuv event loop
  -> OS async APIs
  -> libuv thread pool for some tasks
```

## Что может уходить в thread pool

Типичные категории:

- часть операций `fs`;
- некоторые crypto-операции;
- DNS через `dns.lookup`;
- zlib-сжатие.

```js
import { pbkdf2 } from "node:crypto";

pbkdf2("password", "salt", 100000, 64, "sha512", () => {
  console.log("done");
});
```

Такая операция не должна блокировать основной JS-поток.

## Размер thread pool

Размер thread pool можно менять через `UV_THREADPOOL_SIZE`.

```bash
UV_THREADPOOL_SIZE=8 node server.js
```

Но это не магическая оптимизация: больше потоков может помочь одним задачам и навредить другим из-за конкуренции за CPU.

## Сеть и thread pool

Сетевые операции часто используют неблокирующие возможности ОС и не обязательно занимают thread pool.

## Мини-шпаргалка

- libuv обеспечивает event loop Node.js.
- Thread pool нужен для части fs, crypto, dns, zlib.
- JS callback возвращается в основной поток.
- `UV_THREADPOOL_SIZE` меняет размер пула.
- CPU-heavy JS все равно блокирует event loop, если не вынести его в worker.
