# Как делать HTTP-запросы через fetch в Node.js?

> [!NOTE]
> В современных версиях Node.js доступен глобальный `fetch`, похожий на браузерный Fetch API. Внутри Node.js он опирается на Undici и удобен для HTTP-запросов без установки `axios` или `node-fetch`.

## GET-запрос

```js
const response = await fetch('https://api.example.com/users');

if (!response.ok) {
  throw new Error(`HTTP ${response.status}`);
}

const users = await response.json();

console.log(users);
```

## POST JSON

```js
const response = await fetch('https://api.example.com/users', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({ name: 'Анна' }),
});

const user = await response.json();
```

## Timeout через AbortController

```js
const controller = new AbortController();
const timeout = setTimeout(() => controller.abort(), 5000);

try {
  const response = await fetch('https://api.example.com', {
    signal: controller.signal,
  });

  console.log(response.status);
} finally {
  clearTimeout(timeout);
}
```

## Важный нюанс

`fetch` не бросает ошибку на HTTP-статусы `404` или `500`. Ошибка будет только на сетевом уровне или при abort. Поэтому проверяй `response.ok`.

## Мини-шпаргалка

- `fetch` доступен глобально в современном Node.js.
- Проверяй `response.ok`.
- JSON отправляют через `body: JSON.stringify(data)`.
- Timeout делают через `AbortController`.
- Для продвинутого HTTP-клиента можно использовать Undici напрямую.
