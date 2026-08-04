# Что такое error-first callback?

> [!NOTE]
> Error-first callback - классический Node.js-паттерн, где первым аргументом callback-функции передается ошибка, а следующими аргументами - успешный результат.

## Формат

```js
operation((error, result) => {
  if (error) {
    // обработка ошибки
    return;
  }

  // работа с result
});
```

Первый аргумент зарезервирован под ошибку. Если ошибки нет, обычно передается `null`.

## Пример с fs

```js
import fs from 'node:fs';

fs.readFile('notes.txt', 'utf8', (error, text) => {
  if (error) {
    console.error('Ошибка чтения:', error.message);
    return;
  }

  console.log(text);
});
```

## Почему этот паттерн появился?

В раннем Node.js Promise еще не были стандартным способом писать асинхронный код. Callback API позволял передавать функцию, которую Node.js вызовет после завершения операции.

## Как перейти к Promise?

Многие callback-функции можно обернуть через `promisify`.

```js
import fs from 'node:fs';
import { promisify } from 'node:util';

const readFile = promisify(fs.readFile);

const text = await readFile('notes.txt', 'utf8');
```

Но для `fs` чаще проще сразу взять `node:fs/promises`.

## Мини-шпаргалка

- Первый аргумент callback - ошибка.
- Если ошибки нет, первым аргументом обычно будет `null`.
- После обработки ошибки делай `return`, чтобы не продолжить выполнение.
- Это старый, но все еще распространенный Node.js-паттерн.
- В новом коде чаще используют Promise и `async/await`.
