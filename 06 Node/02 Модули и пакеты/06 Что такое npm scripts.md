> [!summary]
> `npm scripts` - команды проекта, описанные в `package.json`. Они позволяют запускать приложение, тесты, сборку, линтеры, миграции и другие повторяемые действия через `npm run`.

## Где описываются scripts?

```json
{
  "scripts": {
    "dev": "node --watch src/index.js",
    "start": "node src/index.js",
    "test": "node --test",
    "lint": "eslint ."
  }
}
```

Запуск:

```bash
npm run dev
npm test
npm start
```

`test`, `start`, `stop` и некоторые другие scripts можно запускать без слова `run`.

## Зачем scripts нужны?

- стандартизируют команды проекта;
- прячут длинные CLI-команды;
- упрощают onboarding;
- используются в CI/CD;
- уменьшают зависимость от глобально установленных утилит.

## Локальные бинарники

Если пакет установлен в `devDependencies`, его CLI доступен внутри npm script.

```json
{
  "devDependencies": {
    "eslint": "^9.0.0"
  },
  "scripts": {
    "lint": "eslint ."
  }
}
```

Не нужно ставить `eslint` глобально.

## Передача аргументов

```bash
npm run test -- --watch
```

Все после `--` передается внутрь команды.

## Мини-шпаргалка

- Scripts живут в `package.json`.
- Запуск обычного script: `npm run name`.
- `npm test` и `npm start` - короткие формы.
- Локальные CLI из `node_modules/.bin` доступны в scripts.
- В CI лучше запускать те же scripts, что и локально.

