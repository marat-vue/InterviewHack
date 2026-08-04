> [!summary]
> `fs` - встроенный модуль Node.js для работы с файловой системой: файлами, папками, правами, метаданными и потоками чтения/записи. `fs/promises` - promise-версия этого API, которую удобно использовать вместе с `async/await`.

## Главное определение

В браузере JavaScript не имеет прямого доступа к диску пользователя. В Node.js такой доступ есть через модуль `node:fs`.

У `fs` есть несколько стилей API:

| Стиль | Пример | Когда использовать |
|---|---|---|
| Callback API | `fs.readFile(path, cb)` | В старом коде и библиотеках |
| Promise API | `await fs.readFile(path)` из `node:fs/promises` | В современном приложении |
| Sync API | `fs.readFileSync(path)` | В CLI, скриптах и при старте приложения |
| Stream API | `fs.createReadStream(path)` | Для больших файлов |

## Пример чтения файла

```js
import { readFile } from 'node:fs/promises';

const text = await readFile('notes.txt', 'utf8');

console.log(text);
```

Если не указать `'utf8'`, Node вернет `Buffer`, а не строку.

```js
const data = await readFile('image.png');

console.log(Buffer.isBuffer(data)); // true
```

## Почему лучше начинать с fs/promises?

`fs/promises` проще читать, легче комбинируется с `try/catch` и не создает вложенность callback-функций.

```js
import { writeFile } from 'node:fs/promises';

try {
  await writeFile('result.txt', 'Готово', 'utf8');
  console.log('Файл записан');
} catch (error) {
  console.error('Не удалось записать файл:', error.message);
}
```

## Мини-шпаргалка

- `node:fs` - базовый модуль файловой системы.
- `node:fs/promises` - современный promise-интерфейс.
- `readFile` читает файл целиком в память.
- `writeFile` создает или перезаписывает файл.
- Для больших файлов лучше использовать streams.
