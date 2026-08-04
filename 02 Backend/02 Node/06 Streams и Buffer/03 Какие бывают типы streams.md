# Какие бывают типы streams?

> [!NOTE]
> В Node.js есть четыре основных типа streams: readable, writable, duplex и transform. Они отличаются направлением потока данных и тем, можно ли данные изменять по пути.

## Основные типы

| Тип | Что делает | Пример |
|---|---|---|
| `Readable` | Из него читают данные | `fs.createReadStream` |
| `Writable` | В него пишут данные | `fs.createWriteStream` |
| `Duplex` | Можно и читать, и писать | TCP socket |
| `Transform` | Изменяет данные между входом и выходом | gzip, crypto |

## Readable

```js
import { createReadStream } from 'node:fs';

const readable = createReadStream('input.txt', 'utf8');

readable.on('data', (chunk) => {
  console.log(chunk);
});
```

## Writable

```js
import { createWriteStream } from 'node:fs';

const writable = createWriteStream('output.txt');

writable.write('Первая строка\n');
writable.write('Вторая строка\n');
writable.end();
```

## Transform

Transform stream получает данные, преобразует их и передает дальше.

```js
import { createReadStream, createWriteStream } from 'node:fs';
import { createGzip } from 'node:zlib';

createReadStream('app.log')
  .pipe(createGzip())
  .pipe(createWriteStream('app.log.gz'));
```

## Собеседовательный ответ

Если коротко: readable - источник, writable - приемник, duplex - двусторонний канал, transform - двусторонний stream, который меняет данные.

## Мини-шпаргалка

- `Readable` - читаем.
- `Writable` - пишем.
- `Duplex` - читаем и пишем независимо.
- `Transform` - читаем, меняем, пишем.
- `pipe` соединяет streams в цепочку.
