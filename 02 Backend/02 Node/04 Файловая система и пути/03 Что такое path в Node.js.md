> [!summary]
> `path` - встроенный модуль Node.js для безопасной работы с путями к файлам и папкам. Он помогает собирать, разбирать, нормализовать и сравнивать пути без ручной склейки строк.

## Зачем нужен path?

Пути отличаются в разных операционных системах:

| ОС | Разделитель |
|---|---|
| Windows | `\` |
| macOS/Linux | `/` |

Если писать путь руками, код легко сделать хрупким:

```js
const filePath = __dirname + '/data/users.json';
```

Лучше использовать `path.join` или `path.resolve`.

```js
import path from 'node:path';

const filePath = path.join(process.cwd(), 'data', 'users.json');
```

## join vs resolve

`path.join` собирает части пути и нормализует результат.

```js
path.join('data', 'users', '..', 'posts.json');
// data/posts.json
```

`path.resolve` строит абсолютный путь, начиная от текущей рабочей директории или от переданного абсолютного пути.

```js
path.resolve('data', 'users.json');
// C:\project\data\users.json на Windows
```

## Полезные методы

| Метод | Что делает |
|---|---|
| `path.basename(file)` | Имя файла |
| `path.dirname(file)` | Папка файла |
| `path.extname(file)` | Расширение |
| `path.parse(file)` | Разобрать путь на части |
| `path.format(obj)` | Собрать путь из частей |

```js
import path from 'node:path';

const file = '/app/src/index.js';

console.log(path.basename(file)); // index.js
console.log(path.extname(file)); // .js
console.log(path.dirname(file)); // /app/src
```

## Мини-шпаргалка

- `path` убирает ручную склейку путей.
- `join` собирает относительный или абсолютный путь из частей.
- `resolve` возвращает абсолютный путь.
- Для кроссплатформенного кода не полагайся на `/` или `\` вручную.
- `path.parse` удобен, когда нужно получить имя, расширение и директорию отдельно.
