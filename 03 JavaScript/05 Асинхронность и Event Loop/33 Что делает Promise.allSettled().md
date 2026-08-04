# Что делает Promise.allSettled()?

> [!NOTE] Коротко
> `Promise.allSettled()` ждет завершения всех промисов и возвращает результат каждого: успех или ошибку.

## Вопрос

Чем `Promise.allSettled()` отличается от `Promise.all()`?

## Определение

`Promise.allSettled(iterable)` возвращает промис, который всегда успешно завершается массивом результатов, когда все переданные промисы стали `settled`.

Для каждого промиса результат содержит:

- `status: 'fulfilled'` и `value`;
- или `status: 'rejected'` и `reason`.

## Пример

```javascript
const results = await Promise.allSettled([
  Promise.resolve('ok'),
  Promise.reject(new Error('fail')),
]);

console.log(results);
// [
//   { status: 'fulfilled', value: 'ok' },
//   { status: 'rejected', reason: Error('fail') },
// ]
```

## Отличие от Promise.all()

```javascript
Promise.all([
  Promise.resolve('ok'),
  Promise.reject(new Error('fail')),
]); // общий промис отклонится
```

`Promise.all()` падает при первой ошибке. `Promise.allSettled()` не падает из-за одного неудачного промиса и позволяет посмотреть все результаты.

## Когда использовать

- загрузить несколько независимых ресурсов;
- показать частичные данные;
- собрать отчет об успехах и ошибках;
- выполнить пачку задач, где ошибка одной не должна отменять анализ остальных.

## Мини-шпаргалка

```javascript
const results = await Promise.allSettled(tasks);

const successful = results.filter((item) => item.status === 'fulfilled');
const failed = results.filter((item) => item.status === 'rejected');
```
