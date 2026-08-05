# Как работать с headers, statusCode и body?

> [!NOTE]
> HTTP-ответ состоит из статус-кода, заголовков и тела. В Node.js статус задается через `res.statusCode` или `writeHead`, заголовки через `setHeader`, а тело отправляется через `write` и `end`.

## Статус-код

Статус-код сообщает результат запроса:

| Код | Значение |
|---|---|
| `200` | Успешно |
| `201` | Создано |
| `204` | Успешно, но без тела |
| `400` | Ошибка клиента |
| `401` | Не авторизован |
| `403` | Запрещено |
| `404` | Не найдено |
| `500` | Ошибка сервера |

```js
res.statusCode = 404;
res.end('Not found');
```

## Заголовки

Заголовки описывают формат ответа, кэширование, авторизацию и другие параметры.

```js
res.setHeader('Content-Type', 'application/json; charset=utf-8');
res.setHeader('Cache-Control', 'no-store');
```

После отправки тела часть заголовков уже нельзя менять.

## Тело ответа

```js
const payload = {
  ok: true,
  data: [1, 2, 3],
};

res.setHeader('Content-Type', 'application/json; charset=utf-8');
res.end(JSON.stringify(payload));
```

Для HTML:

```js
res.setHeader('Content-Type', 'text/html; charset=utf-8');
res.end('<h1>Hello</h1>');
```

## Чтение JSON body

```js
async function readJson(req) {
  const chunks = [];

  for await (const chunk of req) {
    chunks.push(chunk);
  }

  return JSON.parse(Buffer.concat(chunks).toString('utf8'));
}
```

В реальном сервере нужно ограничивать размер body, иначе клиент может отправить слишком большой запрос.

## Мини-шпаргалка

- Статус: `res.statusCode = 200`.
- Заголовок: `res.setHeader(name, value)`.
- JSON-ответ: `Content-Type: application/json`.
- Тело ответа завершается через `res.end(body)`.
- Размер входящего body нужно ограничивать.
