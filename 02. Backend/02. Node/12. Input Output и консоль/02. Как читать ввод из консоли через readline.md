# Как читать ввод из консоли через readline?

> [!NOTE]
> `node:readline` позволяет читать данные из `process.stdin` построчно. Promise-версия `node:readline/promises` особенно удобна для задач лайвкодинга, где нужно спросить пользователя и дождаться ответа.

## Один вопрос пользователю

```js
import * as readline from 'node:readline/promises';
import { stdin as input, stdout as output } from 'node:process';

const rl = readline.createInterface({ input, output });

const name = await rl.question('Введите имя: ');

console.log(`Привет, ${name}`);
rl.close();
```

Важно вызвать `rl.close()`, иначе процесс может продолжить ждать ввод.

## Несколько вопросов

```js
import * as readline from 'node:readline/promises';
import { stdin as input, stdout as output } from 'node:process';

const rl = readline.createInterface({ input, output });

try {
  const a = Number(await rl.question('a = '));
  const b = Number(await rl.question('b = '));

  console.log(a + b);
} finally {
  rl.close();
}
```

`finally` гарантирует закрытие интерфейса даже при ошибке.

## Callback-версия

```js
import { createInterface } from 'node:readline';

const rl = createInterface({
  input: process.stdin,
  output: process.stdout,
});

rl.question('Возраст: ', (answer) => {
  console.log(Number(answer));
  rl.close();
});
```

## Мини-шпаргалка

- `readline` читает input построчно.
- Для async/await используй `node:readline/promises`.
- Не забывай `rl.close()`.
- В лайвкодинге удобно оборачивать вопросы в `try/finally`.
- Все ответы из консоли приходят строками.
