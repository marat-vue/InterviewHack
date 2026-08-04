# Что делает Promise.all()?

> [!NOTE] Коротко
> `Promise.all()` ждет успешного выполнения всех промисов и возвращает массив результатов. Если один промис отклонится, общий промис тоже отклонится.

## Вопрос

Что произойдет, если один из промисов внутри `Promise.all()` завершится ошибкой?

## Определение

`Promise.all(iterable)` принимает набор промисов или обычных значений и возвращает новый промис.

Он выполнится успешно, когда успешно завершатся все входные промисы. Результаты будут в массиве в том же порядке, в котором промисы были переданы.

## Пример успеха

```javascript
const result = await Promise.all([
  Promise.resolve('user'),
  Promise.resolve('posts'),
  Promise.resolve('comments'),
]);

console.log(result); // ['user', 'posts', 'comments']
```

## Если один промис упал

```javascript
try {
  await Promise.all([
    fetchUser(),
    fetchPosts(),
    Promise.reject(new Error('Comments failed')),
  ]);
} catch (error) {
  console.error(error.message); // 'Comments failed'
}
```

`Promise.all()` отклоняется при первой ошибке. Остальные операции при этом не отменяются автоматически, они просто больше не влияют на результат общего промиса.

## Когда использовать

- несколько независимых запросов;
- параллельная загрузка данных;
- когда результат нужен только если все операции успешны.

## Мини-шпаргалка

```javascript
const [user, posts] = await Promise.all([
  loadUser(),
  loadPosts(),
]);
```
