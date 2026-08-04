# Как устроена структура Nuxt проекта?

> [!NOTE]
> Nuxt использует соглашения по папкам. `app/` содержит Vue-приложение, `server/` содержит Nitro API и server middleware, `shared/` содержит общий код, `public/` отдает статические файлы, а `nuxt.config.ts` управляет конфигурацией.

## Базовая структура

```text
project/
  app/
    app.vue
    pages/
    layouts/
    components/
    composables/
    middleware/
    plugins/
    utils/
    assets/
  server/
    api/
    routes/
    middleware/
    plugins/
    utils/
  shared/
    utils/
    types/
  public/
  nuxt.config.ts
  app.config.ts
```

## Что лежит в `app/`?

`app/` - клиентское и SSR Vue-приложение:

- pages;
- layouts;
- components;
- composables;
- route middleware;
- Vue plugins;
- assets;
- frontend utilities.

## Что лежит в `server/`?

`server/` - Nitro server:

- API endpoints;
- server routes;
- server middleware;
- Nitro plugins;
- server-only utilities.

Код из `server/` не попадает в client bundle.

## Что лежит в `shared/`?

`shared/` нужен для кода, который может использоваться и app bundle, и Nitro server bundle:

- types;
- validation schemas;
- pure utilities.

Туда нельзя класть код, который зависит только от browser или только от server.

## Мини-шпаргалка

- `app/` - Vue-приложение.
- `server/` - Nitro backend.
- `shared/` - общий безопасный код.
- `public/` - файлы отдаются как static assets.
- `.nuxt/` и `.output/` генерируются автоматически.
