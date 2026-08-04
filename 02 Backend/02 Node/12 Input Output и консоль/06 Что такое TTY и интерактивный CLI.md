# Что такое TTY и интерактивный CLI?

> [!NOTE]
> TTY - терминальное устройство. В Node.js можно проверить, запущена ли программа интерактивно в терминале, через `process.stdin.isTTY` и `process.stdout.isTTY`.

## Зачем знать про TTY?

CLI-программа может работать в двух режимах:

```bash
node cli.js
```

Интерактивный режим: пользователь вводит данные руками.

```bash
cat input.txt | node cli.js
```

Pipe-режим: программа получает данные из другого процесса.

## Проверка

```js
if (process.stdin.isTTY) {
  console.log('Интерактивный ввод');
} else {
  console.log('Данные пришли через pipe');
}
```

## Пример выбора режима

```js
import { readFileSync } from 'node:fs';
import * as readline from 'node:readline/promises';
import { stdin as input, stdout as output } from 'node:process';

if (process.stdin.isTTY) {
  const rl = readline.createInterface({ input, output });
  const name = await rl.question('Имя: ');
  console.log(`Привет, ${name}`);
  rl.close();
} else {
  const text = readFileSync(0, 'utf8');
  console.log(text.toUpperCase());
}
```

## Мини-шпаргалка

- TTY означает интерактивный терминал.
- `process.stdin.isTTY` помогает отличить ручной ввод от pipe.
- CLI может поддерживать оба режима.
- Цветной вывод обычно включают только для TTY.
- В automated output лучше не добавлять лишние prompts.
