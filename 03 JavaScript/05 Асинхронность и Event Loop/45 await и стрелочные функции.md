# await и стрелочные функции

> [!NOTE] Коротко
> `await` можно использовать в стрелочной функции, если она объявлена как `async`.

## Вопрос

Можно ли использовать `await` в стрелочных функциях?

## Определение

Стрелочная функция может быть асинхронной. Для этого перед параметрами нужно поставить `async`.

Внутри такой функции можно использовать `await`, а сама функция всегда будет возвращать `Promise`.

## Пример

```javascript
const loadUser = async () => {
  const response = await fetch('/api/user');
  const user = await response.json();

  return user;
};
```

## Один параметр

```javascript
const getPost = async (id) => {
  const response = await fetch(`/api/posts/${id}`);

  return response.json();
};
```

С `async` скобки вокруг одного параметра обычно оставляют для читаемости.

## Короткая запись

```javascript
const getJson = async (url) => (await fetch(url)).json();
```

Так писать можно, но в сложной логике лучше использовать обычное тело функции с `try...catch`.

## Частая ошибка в map

```javascript
const users = await Promise.all(
  ids.map(async (id) => {
    const response = await fetch(`/api/users/${id}`);
    return response.json();
  })
);
```

`map(async ...)` возвращает массив промисов, поэтому для получения значений нужен `Promise.all()`.

## Мини-шпаргалка

```javascript
const fn = async () => {
  const value = await promise;
  return value;
};
```
