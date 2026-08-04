# Как настроить sitemap в Nuxt?

> [!NOTE]
> Sitemap помогает поисковикам находить URL сайта. В Nuxt его удобно генерировать через Nuxt SEO или модуль `@nuxtjs/sitemap`, который создает best-practice XML sitemap и умеет работать с routes, images, i18n и sources.

## Зачем нужен sitemap?

Sitemap отвечает:

```text
Какие URL есть на сайте и какие из них нужно обходить?
```

Он особенно полезен для:

- больших сайтов;
- blog/content projects;
- ecommerce;
- страниц, которые плохо связаны внутренними ссылками;
- мультиязычных сайтов.

## Через Nuxt SEO

```ts
export default defineNuxtConfig({
  modules: ['@nuxtjs/seo'],
  site: {
    url: 'https://example.com',
    name: 'Example',
  },
});
```

Nuxt SEO подключает sitemap stack.

## Standalone модуль

```bash
npx nuxi@latest module add sitemap
```

Конфигурация:

```ts
export default defineNuxtConfig({
  modules: ['@nuxtjs/sitemap'],
  site: {
    url: 'https://example.com',
  },
});
```

## Динамические URL

Для динамических страниц может понадобиться источник URL:

```ts
export default defineNuxtConfig({
  sitemap: {
    sources: ['/api/__sitemap__/urls'],
  },
});
```

А endpoint вернет список URL.

## Мини-шпаргалка

- Sitemap помогает поисковикам находить страницы.
- Для Nuxt можно использовать `@nuxtjs/seo` или `@nuxtjs/sitemap`.
- Site URL важен для корректных absolute URLs.
- Динамические страницы требуют источника URL.
- Sitemap не гарантирует индексацию, он помогает discovery.
