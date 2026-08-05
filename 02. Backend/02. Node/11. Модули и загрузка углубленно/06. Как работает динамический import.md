# Как работает динамический import?

> [!NOTE]
> Динамический `import()` загружает модуль во время выполнения и возвращает Promise. Он полезен для ленивой загрузки, условного импорта, загрузки ESM из CommonJS и уменьшения стартовой стоимости приложения.

## Базовый пример

```js
const module = await import('./math.js');

console.log(module.sum(2, 3));
```

В отличие от статического `import`, динамический можно вызвать внутри условия или функции.

```js
async function loadFormatter(type) {
  if (type === 'html') {
    return import('./format-html.js');
  }

  return import('./format-text.js');
}
```

## В CommonJS

CommonJS не может использовать статический `import`, но может вызвать динамический `import()`.

```js
async function main() {
  const { default: chalk } = await import('chalk');
  console.log(chalk.green('ok'));
}

main();
```

Это полезно, когда CJS-проекту нужно подключить ESM-only пакет.

## Когда использовать?

- редкая тяжелая зависимость;
- условная загрузка драйвера;
- CLI-команда с несколькими режимами;
- совместимость CJS -> ESM;
- плагины.

## Мини-шпаргалка

- `import()` возвращает Promise.
- Работает и в ESM, и в CommonJS.
- Позволяет загружать модуль условно.
- Может уменьшить стартовое время CLI.
- Ошибки загрузки нужно ловить через `try/catch`.
