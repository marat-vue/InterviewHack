# Что такое Stream в Node.js?

> [!NOTE]
> Stream - это интерфейс для работы с данными по частям. Вместо того чтобы загружать весь файл, запрос или ответ в память, Node.js может читать и передавать данные маленькими порциями.

## Зачем нужны streams?

Если файл весит 5 ГБ, `readFile` попытается прочитать его целиком. Stream позволяет обработать данные постепенно.

```js
import { createReadStream } from 'node:fs';

const stream = createReadStream('big.log', 'utf8');

stream.on('data', (chunk) => {
  console.log('Получен кусок:', chunk.length);
});

stream.on('end', () => {
  console.log('Чтение завершено');
});
```

## Главная идея

Stream похож на ленту данных:

```txt
[chunk] -> [chunk] -> [chunk] -> обработчик
```

Ты работаешь не со всем объемом сразу, а с текущим фрагментом.

## Async iteration

Современный способ читать stream:

```js
import { createReadStream } from 'node:fs';

const stream = createReadStream('big.log', 'utf8');

for await (const chunk of stream) {
  console.log(chunk.length);
}
```

Такой код проще, чем обработчики `data`, `end` и `error`.

## Почему streams важны для backend?

Streams используются в:

- чтении и записи файлов;
- HTTP request и response;
- загрузке файлов;
- проксировании;
- архивации и сжатии;
- работе с большими JSON/CSV/log-файлами.

## Мини-шпаргалка

- Stream обрабатывает данные частями.
- Streams экономят память.
- `chunk` часто является `Buffer`.
- Streams особенно важны для больших файлов и сетевых данных.
- Читать stream можно через события или `for await`.
