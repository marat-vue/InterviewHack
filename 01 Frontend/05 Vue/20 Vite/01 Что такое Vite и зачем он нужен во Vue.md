# Что такое Vite и зачем он нужен во Vue?

> [!NOTE]
> Vite - современный frontend build tool и dev server. В Vue-проектах он отвечает за запуск разработки, HMR, обработку `.vue` файлов, TypeScript, CSS, assets, env variables и production build.

## Из чего состоит Vite?

Vite можно понимать как две части:

```txt
Development:
  dev server + native ES modules + HMR

Production:
  bundling + optimization + static assets
```

В dev режиме Vite не собирает все приложение в один большой bundle заранее. Он отдает modules браузеру по запросу, поэтому старт проекта быстрый.

## Почему Vite популярен во Vue?

- быстро стартует dev server;
- быстро обновляет изменения через HMR;
- официально дружит с Vue через `@vitejs/plugin-vue`;
- просто работает с TypeScript;
- удобно подключает CSS preprocessors и PostCSS/Tailwind;
- собирает production build через Rollup/Rolldown-экосистему.

## Создание Vue проекта

```bash
npm create vite@latest my-vue-app -- --template vue-ts
cd my-vue-app
npm install
npm run dev
```

Для JavaScript:

```bash
npm create vite@latest my-vue-app -- --template vue
```

## Главные файлы

```txt
index.html
vite.config.ts
src/
  main.ts
  App.vue
```

В Vite `index.html` - важная точка входа, а не просто файл в `public`.

## Мини-шпаргалка

- Vite - dev server и build tool.
- В dev режиме использует native ESM.
- HMR обновляет изменения без полной перезагрузки.
- Vue подключается через `@vitejs/plugin-vue`.
- Production build обычно запускается через `vite build`.
