# Блокировка текущей функции с await

> [!NOTE]
> `await` приостанавливает только текущую async-функцию, но не блокирует весь JavaScript-поток.

## Вопрос

Почему говорят, что `await` "блокирует" только текущую функцию?

## Определение

Когда выполнение доходит до `await`, текущая async-функция ставится на паузу до завершения промиса. Но Call Stack освобождается, и Event Loop может выполнять другие задачи: события, таймеры, другие промисы.

Поэтому `await` не равен синхронной блокировке.

## Пример

```javascript
async function run() {
  console.log('before await');

  await new Promise((resolve) => setTimeout(resolve, 1000));

  console.log('after await');
}

run();

console.log('outside');

// before await
// outside
// after await
```

Пока `run()` ждет промис, внешний код продолжает выполняться.

## Последовательные await могут замедлять

```javascript
const user = await loadUser();
const posts = await loadPosts();
```

Если задачи независимы, второй `await` зря ждет первый.

```javascript
const [user, posts] = await Promise.all([
  loadUser(),
  loadPosts(),
]);
```

Так обе операции стартуют параллельно.

## Что await действительно блокирует

`await` блокирует дальнейшие строки внутри текущей async-функции.

```javascript
await loadData();
renderData(); // выполнится после loadData
```

## Мини-шпаргалка

```javascript
await promise; // пауза текущей async-функции, не всего потока
```
