# Что такое встроенный test runner node test?

> [!NOTE]
> В Node.js есть встроенный test runner, который запускается командой `node --test`. Он позволяет писать тесты без обязательной установки Jest, Vitest или Mocha.

## Минимальный тест

```js
import test from 'node:test';
import assert from 'node:assert/strict';

test('sum adds two numbers', () => {
  assert.equal(2 + 2, 4);
});
```

Запуск:

```bash
node --test
```

Node.js найдет тестовые файлы по стандартным шаблонам и запустит их.

## Async-тест

```js
import test from 'node:test';
import assert from 'node:assert/strict';

async function getUser() {
  return { id: 1, name: 'Анна' };
}

test('getUser returns user', async () => {
  const user = await getUser();

  assert.deepEqual(user, { id: 1, name: 'Анна' });
});
```

## subtest

```js
import test from 'node:test';
import assert from 'node:assert/strict';

test('math', async (t) => {
  await t.test('addition', () => {
    assert.equal(1 + 1, 2);
  });
});
```

## Когда хватает встроенного runner?

Он хорош для:

- библиотек;
- утилит;
- backend-модулей;
- небольших сервисов;
- проектов, где не нужны тяжелые UI-возможности тестового фреймворка.

## Мини-шпаргалка

- Запуск: `node --test`.
- Тесты пишутся через `node:test`.
- Проверки удобно делать через `node:assert/strict`.
- Поддерживаются async-тесты.
- Для сложного frontend-окружения чаще берут Vitest или Jest.
