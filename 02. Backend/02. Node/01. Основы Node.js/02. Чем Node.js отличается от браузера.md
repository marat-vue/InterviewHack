# Чем Node.js отличается от браузера?

> [!NOTE]
> Node.js и браузер выполняют JavaScript, но дают разные окружения: браузер работает с DOM и Web API, а Node.js - с файловой системой, сетью, процессом, потоками и серверными API.

## Главное

Один и тот же JavaScript-язык может выполняться в разных runtime.

```text
JavaScript language
  -> Browser runtime
  -> Node.js runtime
```

## Что есть в браузере

- `window`;
- `document`;
- DOM;
- CSSOM;
- события UI;
- `localStorage`;
- `fetch`;
- Web APIs.

```js
document.querySelector("button");
```

В Node.js такого API нет, потому что нет страницы и DOM.

## Что есть в Node.js

- `process`;
- `Buffer`;
- `node:fs`;
- `node:path`;
- `node:http`;
- `node:stream`;
- `node:child_process`;
- `node:worker_threads`.

```js
import { readFile } from "node:fs/promises";

const text = await readFile("notes.txt", "utf8");
```

## Модули

В браузере исторически используются ES Modules.

```js
import { sum } from "./sum.js";
```

В Node.js есть две системы модулей: CommonJS и ES Modules.

```js
const fs = require("node:fs");
```

```js
import fs from "node:fs";
```

## Практический вывод

Frontend-разработчик в Node.js должен помнить: язык знакомый, но окружение другое. Ошибки часто возникают, когда код ожидает DOM в Node.js или Node API в браузере.

## Мини-шпаргалка

- Браузер дает DOM, Node.js дает серверные API.
- В Node.js нет `window` и `document`.
- В Node.js есть `process`, `fs`, `path`, `http`.
- Оба окружения поддерживают современный JavaScript.
- Код зависит не только от языка, но и от runtime.
