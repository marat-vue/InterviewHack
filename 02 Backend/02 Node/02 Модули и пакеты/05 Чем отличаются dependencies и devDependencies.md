# Чем отличаются dependencies и devDependencies?

> [!NOTE]
> `dependencies` - это пакеты, которые нужны приложению во время работы, а `devDependencies` - инструменты, которые нужны только для разработки, тестов, сборки и линтинга.

## Главное

```json
{
  "dependencies": {
    "express": "^5.0.0"
  },
  "devDependencies": {
    "vitest": "^3.0.0",
    "eslint": "^9.0.0"
  }
}
```

`express` нужен серверу в runtime. `eslint` нужен разработчику и CI, но не самому приложению в production.

## dependencies

Сюда кладут то, без чего приложение не запустится:

- web-framework;
- клиент базы данных;
- библиотека логирования;
- validation library;
- runtime SDK.

## devDependencies

Сюда кладут инструменты разработки:

- test runner;
- TypeScript;
- ESLint;
- Prettier;
- bundler;
- генераторы типов.

## Почему это важно

В production-сборках часто устанавливают только production-зависимости.

```bash
npm install --omit=dev
```

Если runtime-пакет случайно лежит в `devDependencies`, приложение может сломаться на сервере.

## Версионные диапазоны

```json
{
  "dependencies": {
    "lodash": "^4.17.21"
  }
}
```

Символ `^` разрешает совместимые обновления по semver. Точный результат установки фиксирует lockfile.

## Мини-шпаргалка

- `dependencies` нужны приложению в runtime.
- `devDependencies` нужны для разработки и CI.
- Сервер может ставить зависимости без dev.
- Ошибка в категории зависимости может сломать deploy.
- Lockfile фиксирует дерево установленных версий.
