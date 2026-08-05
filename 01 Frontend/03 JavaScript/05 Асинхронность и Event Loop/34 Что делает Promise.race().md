# Что делает Promise.race()?

> [!NOTE]
> `Promise.race()` возвращает результат первого завершившегося промиса: успешный или ошибочный.

## Вопрос

Как работает `Promise.race()` и когда он полезен?

## Определение

`Promise.race(iterable)` принимает набор промисов и возвращает новый промис. Он завершается так же, как первый завершившийся входной промис: если первый был `fulfilled`, общий промис успешен; если первый был `rejected`, общий промис отклонен.

## Пример

```javascript
const result = await Promise.race([
  new Promise((resolve) => setTimeout(() => resolve('slow'), 1000)),
  new Promise((resolve) => setTimeout(() => resolve('fast'), 100)),
]);

console.log(result); // 'fast'
```

## Первая ошибка тоже побеждает

```javascript
try {
  await Promise.race([
    new Promise((resolve) => setTimeout(() => resolve('ok'), 1000)),
    Promise.reject(new Error('failed')),
  ]);
} catch (error) {
  console.error(error.message); // 'failed'
}
```

## Пример: таймаут для операции

```javascript
function timeout(ms) {
  return new Promise((_, reject) => {
    setTimeout(() => reject(new Error('Timeout')), ms);
  });
}

const data = await Promise.race([
  fetch('/api/data'),
  timeout(3000),
]);
```

Важно: `Promise.race()` сам по себе не отменяет проигравшие операции.

## Мини-шпаргалка

```javascript
Promise.race(promises); // первый settled: fulfilled или rejected
```
