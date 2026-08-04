# Что такое main, exports и imports в package.json?

> [!NOTE]
> `main`, `exports` и `imports` управляют тем, какие файлы пакета доступны для загрузки. `main` задает старую точку входа, `exports` явно описывает публичный API пакета, а `imports` задает внутренние алиасы.

## main

`main` - классический способ указать entry point пакета.

```json
{
  "name": "my-lib",
  "main": "./dist/index.cjs"
}
```

Если другой проект сделает `require('my-lib')`, Node.js пойдет в этот файл.

## exports

`exports` современнее и строже. Он ограничивает, какие пути доступны извне.

```json
{
  "name": "my-lib",
  "exports": {
    ".": "./dist/index.js",
    "./format": "./dist/format.js"
  }
}
```

Теперь можно:

```js
import { format } from 'my-lib/format';
```

Но нельзя импортировать случайный внутренний файл, если он не экспортирован.

## imports

`imports` задает приватные алиасы внутри пакета. Такие имена начинаются с `#`.

```json
{
  "imports": {
    "#db": "./src/db.js"
  }
}
```

```js
import { db } from '#db';
```

## Мини-шпаргалка

- `main` - старая точка входа.
- `exports` - явный публичный API пакета.
- `imports` - внутренние алиасы пакета.
- `exports` помогает не ломать пользователей случайными internal imports.
- Для библиотек `exports` почти всегда полезен.
