> [!summary]
> JSON-файл в Node.js обычно читают как строку через `fs/promises`, затем преобразуют в объект через `JSON.parse`. Для записи объект превращают в строку через `JSON.stringify`.

## Чтение JSON

```js
import { readFile } from 'node:fs/promises';

const raw = await readFile('users.json', 'utf8');
const users = JSON.parse(raw);

console.log(users);
```

Важно указывать `'utf8'`, иначе вернется `Buffer`.

## Запись JSON

```js
import { writeFile } from 'node:fs/promises';

const user = {
  id: 1,
  name: 'Анна',
};

await writeFile('user.json', JSON.stringify(user, null, 2), 'utf8');
```

Аргументы `null, 2` делают JSON читаемым:

```json
{
  "id": 1,
  "name": "Анна"
}
```

## Обработка ошибок

Ошибки могут возникнуть при чтении файла, отсутствии прав или невалидном JSON.

```js
try {
  const raw = await readFile('settings.json', 'utf8');
  const settings = JSON.parse(raw);
  console.log(settings);
} catch (error) {
  console.error('Не удалось прочитать настройки:', error.message);
}
```

## Почему не всегда стоит использовать import?

В ESM можно импортировать JSON с import attributes, но для конфигов, которые могут меняться во время работы приложения, чтение через `fs` часто понятнее. Импорт модулей кэшируется, а `readFile` каждый раз читает актуальное содержимое файла.

## Мини-шпаргалка

- Чтение: `readFile` + `JSON.parse`.
- Запись: `JSON.stringify` + `writeFile`.
- Для красивого файла используй `JSON.stringify(data, null, 2)`.
- Оборачивай чтение и парсинг в `try/catch`.
- Не используй JSON-файлы как базу данных для конкурентных записей.

