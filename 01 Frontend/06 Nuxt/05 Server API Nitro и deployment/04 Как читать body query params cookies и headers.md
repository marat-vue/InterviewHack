# Как читать body, query, params, cookies и headers?

> [!NOTE]
> В Nuxt server handlers используют h3 utilities: `readBody`, `getQuery`, `getRouterParam`, `getCookie`, `setCookie`, `getHeader`, `setHeader`. Они помогают работать с HTTP request и response внутри `defineEventHandler`.

## Body

```ts
export default defineEventHandler(async (event) => {
  const body = await readBody(event);

  return {
    received: body,
  };
});
```

## Query

```ts
export default defineEventHandler((event) => {
  const query = getQuery(event);

  return {
    page: query.page ?? '1',
  };
});
```

## Route params

```ts
// server/api/users/[id].get.ts
export default defineEventHandler((event) => {
  const id = getRouterParam(event, 'id');

  return { id };
});
```

## Cookies

```ts
export default defineEventHandler((event) => {
  const session = getCookie(event, 'session');

  setCookie(event, 'lastSeen', new Date().toISOString(), {
    httpOnly: true,
    sameSite: 'lax',
  });

  return { hasSession: Boolean(session) };
});
```

## Headers

```ts
export default defineEventHandler((event) => {
  const userAgent = getHeader(event, 'user-agent');

  setHeader(event, 'x-app-version', '1.0.0');

  return { userAgent };
});
```

## Мини-шпаргалка

- `readBody(event)` читает body.
- `getQuery(event)` читает query.
- `getRouterParam(event, name)` читает params.
- `getCookie` и `setCookie` работают с cookies.
- `getHeader` и `setHeader` работают с headers.
