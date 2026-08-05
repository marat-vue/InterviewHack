# Как устроен Vite проект?

> [!NOTE]
> Vite-проект обычно состоит из `index.html`, `vite.config.ts`, `src/main.ts`, Vue-компонентов, assets и public-файлов. Важно понимать, какие файлы проходят через Vite pipeline, а какие копируются как есть.

## Базовая структура

```txt
my-vue-app/
  index.html
  package.json
  vite.config.ts
  public/
    favicon.svg
  src/
    main.ts
    App.vue
    assets/
      logo.svg
    components/
      BaseButton.vue
    pages/
      HomePage.vue
```

## index.html

```html
<div id="app"></div>
<script type="module" src="/src/main.ts"></script>
```

Vite обрабатывает `index.html` как часть module graph. Script указывает на frontend entry.

## src/main.ts

```typescript
import { createApp } from "vue";
import App from "./App.vue";

createApp(App).mount("#app");
```

Здесь подключают plugins:

- router;
- Pinia;
- Vuetify;
- i18n;
- global styles.

## public

Файлы из `public` копируются в root build output и не проходят через bundler processing.

```txt
public/robots.txt -> dist/robots.txt
```

Используй `public`, когда нужен стабильный путь и не нужна обработка asset.

## src/assets

Assets внутри `src` проходят через Vite processing:

```vue
<template>
  <img src="@/assets/logo.svg" alt="Logo" />
</template>
```

Vite может добавить hash к имени файла в production build.

## Мини-шпаргалка

- `index.html` - entry point Vite.
- `src/main.ts` монтирует Vue app.
- `vite.config.ts` настраивает plugins и build.
- `public` копируется как есть.
- `src/assets` проходит через bundler.
- Plugins подключаются в `main.ts` или `vite.config.ts` в зависимости от задачи.
