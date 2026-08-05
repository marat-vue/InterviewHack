# Как работает caching в Nitro?

> [!NOTE]
> Nitro поддерживает caching на уровне route rules, cached event handlers и storage. В Nuxt чаще всего начинают с `routeRules` для страниц и API, а затем переходят к более точному server-side cache.

## Cache через routeRules

```ts
export default defineNuxtConfig({
  routeRules: {
    '/products/**': { swr: 300 },
    '/api/products': {
      cache: {
        maxAge: 300,
      },
    },
  },
});
```

## Что можно кэшировать?

Хорошие кандидаты:

- публичный каталог;
- blog pages;
- docs;
- sitemap;
- expensive public API;
- external CMS responses.

Плохие кандидаты:

- user profile;
- account settings;
- cart;
- pages with private data;
- admin data.

## Cached handler

Идея:

```ts
export default cachedEventHandler(async () => {
  return await loadExpensivePublicData();
}, {
  maxAge: 60 * 10,
});
```

Так можно кэшировать результат server handler.

## Главный риск

Нельзя случайно кэшировать персональные данные как общий response.

Если route зависит от cookie/session/user, общий cache может стать security bug.

## Мини-шпаргалка

- Route cache можно задавать через `routeRules`.
- Public data кэшировать безопаснее.
- Private user data нельзя кэшировать общим cache.
- SWR/ISR работают на уровне route response.
- Для точного контроля используют server-side cache handlers/storage.
