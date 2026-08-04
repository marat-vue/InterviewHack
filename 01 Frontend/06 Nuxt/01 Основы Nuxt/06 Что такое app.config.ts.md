# Что такое app.config.ts?

> [!NOTE]
> `app.config.ts` хранит публичную конфигурацию приложения, доступную на клиенте и сервере: UI-токены, настройки темы, icon config, значения для компонентов. Его не используют для секретов.

## Для чего нужен `app.config.ts`?

`app.config.ts` удобен для настроек, которые:

- нужны UI;
- не являются секретами;
- должны быть доступны в runtime;
- могут использоваться компонентами и модулями.

Пример:

```ts
// app.config.ts
export default defineAppConfig({
  ui: {
    primary: 'green',
  },
  icon: {
    mode: 'css',
    cssLayer: 'base',
  },
});
```

## Как читать app config?

```vue
<script setup lang="ts">
const appConfig = useAppConfig();
</script>

<template>
  <pre>{{ appConfig.ui.primary }}</pre>
</template>
```

## `app.config.ts` или `runtimeConfig`?

| Задача | Что выбрать |
|---|---|
| публичная тема UI | `app.config.ts` |
| публичный base URL API | `runtimeConfig.public` |
| secret token | `runtimeConfig` server-only |
| настройки Nuxt modules | `nuxt.config.ts` |
| цветовая схема компонентов | `app.config.ts` |

## Что нельзя хранить в app config?

Нельзя хранить:

- API secrets;
- private tokens;
- database URLs;
- service passwords;
- любые значения, которые нельзя показать в браузере.

## Мини-шпаргалка

- `app.config.ts` - публичный runtime config для app/UI.
- Читать через `useAppConfig()`.
- Secrets туда не кладут.
- Для secrets используй server-only `runtimeConfig`.
- UI-модули часто используют `app.config.ts`.
