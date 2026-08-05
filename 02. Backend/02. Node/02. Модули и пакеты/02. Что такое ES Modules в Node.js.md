# Что такое ES Modules в Node.js?

> [!NOTE]
> **ES Modules** - стандартная система модулей JavaScript с `import` и `export`. Node.js поддерживает ESM наряду с CommonJS.

## Главное

```js
// math.js
export function sum(a, b) {
  return a + b;
}
```

```js
// app.js
import { sum } from "./math.js";

console.log(sum(2, 3));
```

## Как включить ESM

Есть несколько явных способов:

```json
{
  "type": "module"
}
```

Или расширение:

```text
app.mjs
```

Файлы `.mjs` всегда считаются ES Modules.

## Импорт встроенных модулей

```js
import { readFile } from "node:fs/promises";
import path from "node:path";
```

Префикс `node:` показывает, что модуль встроенный.

## Важные отличия

В ESM нет CommonJS-переменных `__dirname`, `__filename`, `module`, `exports`, `require` в обычном виде.

Для пути текущего файла используют `import.meta.url`.

```js
import { fileURLToPath } from "node:url";
import { dirname } from "node:path";

const __filename = fileURLToPath(import.meta.url);
const __dirname = dirname(__filename);
```

## Мини-шпаргалка

- ESM использует `import` и `export`.
- В Node.js ESM включают через `"type": "module"` или `.mjs`.
- `.cjs` всегда CommonJS.
- В ESM нет обычного `__dirname`.
- Новые проекты часто выбирают ESM, но CommonJS еще очень распространен.
