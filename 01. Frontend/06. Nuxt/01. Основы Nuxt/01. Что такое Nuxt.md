# Что такое Nuxt?

> [!NOTE]
> Nuxt - это full-stack фреймворк поверх Vue, который дает файловый роутинг, SSR из коробки, auto-imports, data fetching, server API, TypeScript-настройки и production-инструменты без ручной сборки всей инфраструктуры.

## Простое определение

Vue отвечает за UI-компоненты и реактивность. Nuxt добавляет вокруг Vue готовую архитектуру приложения:

- routing;
- layouts;
- SSR;
- SSG/prerender;
- data fetching;
- server routes;
- auto-imports;
- modules;
- SEO;
- deployment через Nitro.

То есть Nuxt - не замена Vue, а фреймворк, который использует Vue как UI-слой.

## Пример минимального Nuxt-приложения

```vue
<!-- app/app.vue -->
<template>
  <main>
    <h1>Привет, Nuxt</h1>
    <NuxtPage />
  </main>
</template>
```

Если есть `app/pages/about.vue`, Nuxt автоматически создаст route `/about`.

## Что Nuxt дает из коробки?

| Возможность | Зачем нужна |
|---|---|
| file-based routing | routes создаются из файлов |
| SSR | HTML создается на сервере |
| auto-imports | меньше ручных imports |
| server API | можно писать backend routes |
| data fetching | SSR-friendly загрузка данных |
| modules | готовые интеграции |
| Nitro | server runtime и deployment |

## Где Nuxt особенно полезен?

- content websites;
- blogs;
- marketing sites;
- ecommerce;
- dashboards;
- SaaS apps;
- hybrid apps, где часть страниц SSR/SSG, а часть SPA;
- проекты, где важны SEO и performance.

## Мини-шпаргалка

- Nuxt = Vue + routing + SSR + server + modules.
- Nuxt подходит не только для сайтов, но и для full-stack приложений.
- SSR включен по умолчанию.
- Файлы и папки в Nuxt имеют соглашения.
- Nitro отвечает за серверную часть Nuxt.
