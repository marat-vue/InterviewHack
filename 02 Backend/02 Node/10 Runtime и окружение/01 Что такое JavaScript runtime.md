# Что такое JavaScript runtime?

> [!NOTE]
> JavaScript runtime - это среда, которая умеет выполнять JavaScript-код и дает ему доступ к дополнительным возможностям: таймерам, файловой системе, сети, процессам, консоли и другим API. Node.js - runtime для запуска JavaScript вне браузера.

## Что входит в runtime?

Сам язык JavaScript описывает синтаксис, типы, функции, объекты, промисы и модули. Но сам по себе язык не знает, что такое файл, HTTP-запрос или таймер.

Runtime добавляет:

| Часть | Пример в Node.js |
|---|---|
| JS-движок | V8 |
| Event loop | Очереди задач и фаз |
| Встроенные API | `fs`, `http`, `path`, `stream` |
| Глобальные объекты | `process`, `Buffer`, `setTimeout` |
| Интеграцию с ОС | файлы, сеть, процессы |

## Node.js vs браузер

```js
// В Node.js
import { readFile } from 'node:fs/promises';

const text = await readFile('notes.txt', 'utf8');
```

```js
// В браузере
const response = await fetch('/notes.txt');
const text = await response.text();
```

Оба примера используют JavaScript, но runtime-окружение разное.

## Что важно на собеседовании?

Если коротко: Node.js - это не язык и не фреймворк. Это runtime, который запускает JavaScript через V8 и добавляет серверные API.

## Мини-шпаргалка

- JavaScript - язык.
- V8 - движок, который выполняет JS.
- Node.js - runtime вокруг V8 и системных API.
- Runtime определяет, какие глобальные объекты и API доступны.
- Один и тот же JS-код может вести себя по-разному в разных runtime.
