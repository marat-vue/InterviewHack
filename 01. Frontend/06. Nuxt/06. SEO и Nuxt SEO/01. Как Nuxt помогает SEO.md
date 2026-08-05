# Как Nuxt помогает SEO?

> [!NOTE]
> Nuxt помогает SEO через SSR/SSG, управление head/meta, sitemap, robots, structured data, OG images и performance. Но Nuxt сам по себе не гарантирует SEO: нужно правильно настроить контент, meta, canonical, индексацию и скорость.

## Почему SSR полезен для SEO?

При SSR поисковик получает готовый HTML:

```html
<h1>Купить механическую клавиатуру</h1>
<p>Каталог клавиатур с фильтрами и доставкой.</p>
```

Это лучше, чем пустой SPA shell:

```html
<div id="app"></div>
```

## Что важно для SEO в Nuxt?

- title;
- meta description;
- canonical URL;
- Open Graph;
- Twitter cards;
- sitemap.xml;
- robots.txt;
- Schema.org;
- правильные status codes;
- отсутствие дублей;
- хорошая скорость.

## SEO не только meta tags

Плохая SEO-страница может иметь SSR, но:

- не иметь нормального H1;
- иметь дубли title;
- отдавать `200` для несуществующих страниц;
- блокироваться robots.txt;
- иметь тяжелые images;
- иметь hydration errors;
- грузить много third-party scripts.

## Nuxt SEO stack

Для production-проектов часто используют:

- `useSeoMeta`;
- `@nuxtjs/seo`;
- Nuxt Sitemap;
- Nuxt Robots;
- Nuxt Schema.org;
- Nuxt OG Image;
- Nuxt Image;
- Nuxt Fonts;
- Nuxt Scripts.

## Мини-шпаргалка

- Nuxt помогает SEO через SSR/SSG.
- SEO требует title, description, canonical, sitemap, robots.
- Structured data помогает поисковикам понимать страницу.
- Performance влияет на качество страницы.
- Nuxt не спасет плохой контент и неправильную индексацию.
