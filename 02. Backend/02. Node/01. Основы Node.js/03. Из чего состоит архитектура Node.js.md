# Из чего состоит архитектура Node.js?

> [!NOTE]
> Архитектура Node.js строится вокруг движка V8, libuv, event loop, встроенных модулей Node.js и JavaScript API, через которые разработчик работает с системой.

## Общая схема

```text
JavaScript code
  -> Node.js API
  -> V8 + C++ bindings
  -> libuv
  -> OS: files, network, timers, threads
```

## V8

V8 исполняет JavaScript: парсит код, компилирует, оптимизирует и выполняет его.

```js
const result = 2 + 2;
```

Этот код исполняется движком V8, как и JavaScript в Chrome.

## libuv

libuv отвечает за event loop, неблокирующий I/O, timers, thread pool и абстракцию над операционной системой.

```js
import { readFile } from "node:fs/promises";

const data = await readFile("data.txt", "utf8");
```

Файловая операция уходит из JS-кода в системный слой, а результат возвращается асинхронно.

## Встроенные модули

Node.js дает стандартную библиотеку:

- `node:fs`;
- `node:path`;
- `node:http`;
- `node:stream`;
- `node:crypto`;
- `node:events`;
- `node:worker_threads`.

## Event loop

Event loop позволяет одному основному JS-потоку обслуживать много асинхронных операций.

```text
call stack empty
  -> event loop takes next callback/task
  -> JS executes callback
```

## Мини-шпаргалка

- V8 исполняет JavaScript.
- libuv дает event loop и async I/O.
- Node API связывает JS-код с системными возможностями.
- Встроенные модули дают серверные инструменты.
- Основной JS-код выполняется в одном потоке, но операции могут уходить в OS/thread pool.
