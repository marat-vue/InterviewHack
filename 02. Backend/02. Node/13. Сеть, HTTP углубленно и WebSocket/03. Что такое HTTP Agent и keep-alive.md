# Что такое HTTP Agent и keep-alive?

> [!NOTE]
> HTTP Agent управляет сетевыми соединениями HTTP-клиента: создает сокеты, переиспользует их, ограничивает количество соединений и помогает работать с keep-alive. Это важно для производительности сервисов, которые часто ходят во внешние API.

## Проблема без переиспользования соединений

Каждый новый TCP/TLS connection стоит времени. Если сервис делает много запросов к одному API, выгодно переиспользовать соединения.

```txt
request -> new TCP -> TLS -> HTTP -> close
request -> new TCP -> TLS -> HTTP -> close
```

С keep-alive:

```txt
TCP/TLS connection -> request -> response -> request -> response
```

## Agent в node:http

```js
import http from 'node:http';

const agent = new http.Agent({
  keepAlive: true,
  maxSockets: 50,
});
```

Agent можно передавать в низкоуровневые HTTP-запросы.

## Современный fetch

Глобальный `fetch` в Node.js работает через Undici. Для тонкой настройки соединений часто используют Undici dispatcher/client/pool напрямую.

## Почему это спрашивают?

Если backend делает много исходящих запросов, плохая настройка соединений может дать:

- лишнюю latency;
- слишком много открытых сокетов;
- исчерпание ресурсов;
- нестабильность под нагрузкой.

## Мини-шпаргалка

- Agent управляет клиентскими HTTP-соединениями.
- Keep-alive переиспользует TCP/TLS connection.
- `maxSockets` ограничивает параллельные сокеты.
- Для `fetch` в Node.js важен Undici.
- На high-load нельзя забывать про лимиты соединений и timeout.
