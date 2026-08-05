# Что такое CommonJS modules?

> [!NOTE]
> **CommonJS** - историческая система модулей Node.js, где зависимости подключают через `require()`, а экспорт делают через `module.exports` или `exports`.

## Главное

```js
// math.js
function sum(a, b) {
  return a + b;
}

module.exports = { sum };
```

```js
// app.js
const { sum } = require("./math.js");

console.log(sum(2, 3));
```

## Как работает require

`require()` загружает модуль, выполняет файл и возвращает то, что записано в `module.exports`.

```js
const fs = require("node:fs");
```

CommonJS синхронный по своей природе, поэтому хорошо подходил для серверного окружения Node.js.

## module.exports и exports

```js
exports.sum = (a, b) => a + b;
```

Это короткая ссылка на `module.exports`, но ее легко сломать, если присвоить `exports` новое значение.

```js
// плохо
exports = { sum };
```

Лучше явно использовать `module.exports`, если экспортируется объект целиком.

## Где встречается

- Старые Node.js-проекты.
- Много npm-пакетов.
- Конфиги инструментов.
- Скрипты без `"type": "module"`.

## Мини-шпаргалка

- CommonJS использует `require()`.
- Экспорт идет через `module.exports`.
- Каждый файл - отдельный модуль.
- Модули кешируются после первого require.
- CommonJS до сих пор часто встречается в Node.js.
