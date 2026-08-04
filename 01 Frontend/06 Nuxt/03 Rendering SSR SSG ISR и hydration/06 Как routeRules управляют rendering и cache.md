# Как routeRules управляют rendering и cache?

> [!NOTE]
> `routeRules` позволяют задавать правила для маршрутов: prerender, SSR off, SWR, ISR, redirects, headers и caching. Это главный механизм hybrid rendering в Nuxt.

## Пример

```ts
export default defineNuxtConfig({
  routeRules: {
    '/': { prerender: true },
    '/blog/**': { isr: 3600 },
    '/products/**': { swr: 300 },
    '/admin/**': { ssr: false },
    '/old-page': { redirect: '/new-page' },
  },
});
```

## Что можно задавать?

| Rule | Смысл |
|---|---|
| `prerender` | сгенерировать route заранее |
| `ssr: false` | рендерить как SPA |
| `swr` | stale-while-revalidate cache |
| `isr` | incremental static regeneration |
| `redirect` | redirect |
| `headers` | добавить response headers |

## Почему это мощно?

Можно не выбирать один режим для всего приложения.

Пример:

```text
/                 -> prerender
/blog/**          -> ISR
/products/**      -> SWR
/account/**       -> SSR
/admin/**         -> CSR
```

Так Nuxt-приложение адаптируется под разные типы страниц.

## Частая ошибка

Не стоит писать:

```ts
'/account/**': { swr: 3600 }
```

если страница показывает персональные данные пользователя. Общий cache может отдать чужой HTML.

## Мини-шпаргалка

- `routeRules` задают поведение per route.
- Это основа hybrid rendering.
- `prerender`, `isr`, `swr`, `ssr: false` решают разные задачи.
- Не кэшируй персонализированные страницы общим cache.
- Route rules зависят от Nitro/deployment preset.

