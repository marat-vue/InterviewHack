# Что такое Nuxt DevTools?

> [!NOTE]
> Nuxt DevTools - визуальные инструменты для анализа Nuxt-приложения: pages, components, imports, modules, payload, runtime config, performance hints и другие сведения, которые помогают понимать проект и искать проблемы.

## Как включить?

```ts
export default defineNuxtConfig({
  devtools: {
    enabled: true,
  },
});
```

После перезапуска dev server панель можно открыть в браузере.

## Зачем нужны DevTools?

Они помогают увидеть:

- routes;
- components;
- auto-imports;
- modules;
- Nitro/API;
- payload;
- app config;
- runtime config public values;
- performance hints.

## Когда особенно полезно?

- изучение чужого Nuxt-проекта;
- debug auto-imports;
- понимание routes;
- проверка modules;
- анализ payload;
- поиск performance gaps.

## Ограничение

Nuxt DevTools - инструмент разработки. Не надо полагаться на него как на production monitoring.

Для production нужны:

- logs;
- error tracking;
- analytics;
- synthetic checks;
- performance monitoring.

## Мини-шпаргалка

- DevTools включаются через `devtools.enabled`.
- Помогают понять структуру Nuxt-приложения.
- Полезны для routes, imports, modules и payload.
- Это dev-only инструмент.
- Для production нужен отдельный monitoring.

