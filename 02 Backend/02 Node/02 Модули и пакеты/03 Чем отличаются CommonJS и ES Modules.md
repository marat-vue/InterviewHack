> [!summary]
> CommonJS использует `require()` и `module.exports`, а ES Modules используют `import` и `export`. В Node.js обе системы поддерживаются, но отличаются синтаксисом, загрузкой, interop и правилами определения типа файла.

## Синтаксис

CommonJS:

```js
const { sum } = require("./math.js");

module.exports = { sum };
```

ES Modules:

```js
import { sum } from "./math.js";

export { sum };
```

## Как Node.js определяет тип модуля

| Маркер | Тип |
| --- | --- |
| `.cjs` | CommonJS |
| `.mjs` | ES Module |
| `.js` + `"type": "commonjs"` | CommonJS |
| `.js` + `"type": "module"` | ES Module |

## Загрузка

CommonJS загружается синхронно через `require()`. ES Modules поддерживают статический анализ импортов и top-level `await`.

```js
const config = await import("./config.js");
```

## Interop

ESM может импортировать CommonJS, но named exports могут быть не всегда такими очевидными. CommonJS может загружать ESM не так же просто, особенно если модуль использует top-level await.

## Что выбрать

Для нового Node.js-проекта часто выбирают ESM, потому что это стандарт JavaScript и он совпадает с браузером. Но при работе с legacy-кодом и старой экосистемой нужно уверенно читать CommonJS.

## Мини-шпаргалка

- CommonJS: `require`, `module.exports`.
- ESM: `import`, `export`.
- `.mjs` всегда ESM.
- `.cjs` всегда CommonJS.
- `"type"` в `package.json` влияет на `.js`.
- На собеседовании важно понимать оба формата.
