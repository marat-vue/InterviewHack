# Что такое встроенные модули Node.js?

> [!NOTE]
> **Встроенные модули Node.js** - это модули стандартной библиотеки, которые доступны без установки из npm: `node:fs`, `node:path`, `node:http`, `node:stream`, `node:crypto` и другие.

## Главное

Встроенный модуль можно импортировать сразу.

```js
import { readFile } from "node:fs/promises";

const text = await readFile("README.md", "utf8");
```

Префикс `node:` явно показывает, что модуль встроенный.

## Частые встроенные модули

| Модуль | Для чего нужен |
| --- | --- |
| `node:fs` | Файловая система |
| `node:path` | Работа с путями |
| `node:http` | HTTP-серверы и клиенты |
| `node:events` | EventEmitter |
| `node:stream` | Потоки данных |
| `node:crypto` | Хеши, случайные значения, криптография |
| `node:process` | Информация о процессе |
| `node:worker_threads` | Параллельные вычисления |
| `node:test` | Встроенный test runner |

## CommonJS пример

```js
const path = require("node:path");

const filePath = path.join("src", "index.js");
```

## Почему node: полезен

```js
import fs from "node:fs";
```

Такой импорт нельзя перепутать с npm-пакетом с похожим именем. Это делает код читаемее и безопаснее.

## Мини-шпаргалка

- Встроенные модули не нужно устанавливать.
- Лучше импортировать их с префиксом `node:`.
- `fs` работает с файлами.
- `path` строит пути.
- `http` позволяет создать сервер.
- `stream`, `events`, `crypto`, `process` часто встречаются в backend-коде.
