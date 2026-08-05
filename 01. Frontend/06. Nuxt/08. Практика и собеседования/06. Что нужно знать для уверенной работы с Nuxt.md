# Что нужно знать для уверенной работы с Nuxt?

> [!NOTE]
> Для уверенной работы с Nuxt нужно понимать Vue, SSR, файловую структуру, data fetching, Nitro server, routeRules, SEO, runtime config, modules, deployment и performance. Одного знания компонентов недостаточно.

## Core skills

Нужно уметь:

- создавать Nuxt project;
- понимать `app/`, `server/`, `shared/`;
- создавать pages и dynamic routes;
- использовать layouts;
- писать middleware;
- подключать plugins;
- работать с `nuxt.config.ts`;
- различать `app.config.ts` и `runtimeConfig`.

## Rendering skills

Нужно объяснять:

- SSR;
- CSR;
- SSG;
- prerender;
- ISR;
- SWR;
- hydration;
- routeRules;
- browser-only code.

## Data skills

Нужно уверенно использовать:

- `useFetch`;
- `useAsyncData`;
- `$fetch`;
- `useState`;
- `useRuntimeConfig`;
- `refreshNuxtData`;
- custom API client.

## Production skills

Нужно понимать:

- SEO;
- sitemap/robots;
- Open Graph;
- images/fonts/scripts optimization;
- server API errors;
- caching;
- deployment output;
- security headers.

## Мини-шпаргалка

- Nuxt требует понимания frontend и server context.
- SSR-safe мышление обязательно.
- Data fetching надо делать через Nuxt payload-aware APIs.
- SEO и performance - не optional для публичных Nuxt сайтов.
- На собеседовании важны trade-offs.
