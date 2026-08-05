# Как настроить robots txt в Nuxt?

> [!NOTE]
> `robots.txt` сообщает crawler-ам, какие разделы сайта можно обходить, а какие нет. В Nuxt его удобно управлять через Nuxt SEO или Nuxt Robots, включая route rules и site config.

## Что делает robots.txt?

Пример:

```text
User-agent: *
Allow: /
Disallow: /admin

Sitemap: https://example.com/sitemap.xml
```

Это не security-механизм. Он не защищает приватные страницы, а только дает инструкцию crawler-ам.

## Через Nuxt SEO

```ts
export default defineNuxtConfig({
  modules: ['@nuxtjs/seo'],
  site: {
    url: 'https://example.com',
  },
});
```

Nuxt SEO подключает Robots module как часть stack.

## Standalone Nuxt Robots

```bash
npx nuxi@latest module add robots
```

Пример идеи:

```ts
export default defineNuxtConfig({
  robots: {
    blockAiBots: true,
  },
});
```

В актуальных версиях robots rules могут настраиваться через `robots.txt`, config или route rules. Смотри docs версии модуля.

## Route rules

Для отдельных routes:

```ts
export default defineNuxtConfig({
  routeRules: {
    '/admin/**': { robots: false },
  },
});
```

## Мини-шпаргалка

- robots.txt управляет crawling, а не реальной безопасностью.
- Закрытые страницы нужно защищать auth, а не robots.
- Nuxt SEO включает Robots module.
- Sitemap URL обычно указывают в robots.txt.
- Для отдельных routes можно использовать `routeRules`.
