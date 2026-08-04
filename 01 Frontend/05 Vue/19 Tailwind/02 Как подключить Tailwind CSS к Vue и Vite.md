# Как подключить Tailwind CSS к Vue и Vite?

> [!NOTE]
> В актуальной версии Tailwind CSS для Vite используют пакет `tailwindcss` и plugin `@tailwindcss/vite`. Plugin добавляют в `vite.config.ts`, а в главный CSS-файл импортируют Tailwind через `@import "tailwindcss"`.

## Установка

```bash
npm install tailwindcss @tailwindcss/vite
```

## vite.config.ts

```typescript
import { defineConfig } from "vite";
import vue from "@vitejs/plugin-vue";
import tailwindcss from "@tailwindcss/vite";

export default defineConfig({
  plugins: [
    vue(),
    tailwindcss(),
  ],
});
```

## Главный CSS-файл

```css
@import "tailwindcss";
```

Например:

```typescript
// src/main.ts
import { createApp } from "vue";
import App from "./App.vue";
import "./style.css";

createApp(App).mount("#app");
```

## Проверка

```vue
<template>
  <h1 class="text-3xl font-bold underline">
    Hello Tailwind
  </h1>
</template>
```

Если текст стал крупным, жирным и подчеркнутым, Tailwind подключен.

## Чем отличается от старых гайдов?

В старых проектах часто встречаются:

- `tailwind.config.js`;
- `postcss.config.js`;
- `@tailwind base`;
- `@tailwind components`;
- `@tailwind utilities`.

В Tailwind CSS v4 для Vite основной путь стал проще: Vite plugin и `@import "tailwindcss"`. Если работаешь со старым проектом, проверяй его версию Tailwind.

## Мини-шпаргалка

- Установка: `npm install tailwindcss @tailwindcss/vite`.
- Plugin: `tailwindcss()` в `vite.config.ts`.
- CSS: `@import "tailwindcss";`.
- Главный CSS нужно импортировать в `main.ts`.
- Старые Tailwind v3 конфиги могут отличаться.
