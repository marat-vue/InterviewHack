# Как работать с __dirname и import.meta.url?

> [!NOTE]
> `__dirname` показывает папку текущего файла в CommonJS. В ES Modules его нет, поэтому обычно используют `import.meta.url` и `fileURLToPath`.

## В CommonJS

В CommonJS доступны специальные переменные:

```js
console.log(__filename); // полный путь к текущему файлу
console.log(__dirname); // папка текущего файла
```

Они удобны для чтения файлов рядом с текущим модулем.

```js
const path = require('node:path');
const fs = require('node:fs');

const filePath = path.join(__dirname, 'template.html');
const html = fs.readFileSync(filePath, 'utf8');
```

## В ES Modules

В ESM `__dirname` и `__filename` не существуют.

```js
import { fileURLToPath } from 'node:url';
import path from 'node:path';

const __filename = fileURLToPath(import.meta.url);
const __dirname = path.dirname(__filename);

console.log(__dirname);
```

`import.meta.url` - это URL текущего модуля, например `file:///C:/project/index.js`, поэтому его нужно преобразовать в обычный путь.

## process.cwd() vs __dirname

| Значение | Что означает |
|---|---|
| `process.cwd()` | Папка, из которой запустили процесс |
| `__dirname` | Папка, где лежит текущий файл |

```js
// Запуск: node src/app.js
console.log(process.cwd()); // корень проекта
console.log(__dirname); // корень проекта/src
```

## Мини-шпаргалка

- `__dirname` есть в CommonJS.
- В ESM используй `import.meta.url`.
- `fileURLToPath(import.meta.url)` превращает URL модуля в путь.
- `process.cwd()` зависит от места запуска команды.
- Для файлов рядом с модулем чаще нужен `__dirname`, а не `cwd`.
