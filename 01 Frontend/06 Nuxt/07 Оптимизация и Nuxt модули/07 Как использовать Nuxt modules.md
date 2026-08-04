# Как использовать Nuxt modules?

> [!NOTE]
> Nuxt modules расширяют приложение: добавляют компоненты, composables, config, server handlers, integrations и build-time поведение. Их подключают в `nuxt.config.ts` через `modules`.

## Пример

```ts
export default defineNuxtConfig({
  modules: [
    '@nuxt/image',
    '@nuxt/icon',
    '@nuxt/fonts',
    '@nuxtjs/seo',
  ],
});
```

## Установка через nuxi

```bash
npx nuxi@latest module add image
npx nuxi@latest module add icon
npx nuxi@latest module add fonts
```

Команда может установить dependency и обновить config.

## Что может делать module?

- регистрировать components;
- добавлять composables;
- добавлять server routes;
- расширять Vite/Nitro config;
- генерировать файлы;
- добавлять DevTools вкладки;
- подключать CSS;
- давать typed config.

## Как выбирать module?

Перед установкой проверь:

- поддерживает ли Nuxt 4/текущую версию;
- активность maintenance;
- docs;
- bundle/runtime impact;
- security;
- нужна ли эта зависимость вообще.

## Мини-шпаргалка

- Modules подключаются в `nuxt.config.ts`.
- `nuxi module add` упрощает установку.
- Modules могут менять build и runtime.
- Не ставь модуль ради одной маленькой функции.
- Проверяй compatibility и влияние на bundle/performance.
