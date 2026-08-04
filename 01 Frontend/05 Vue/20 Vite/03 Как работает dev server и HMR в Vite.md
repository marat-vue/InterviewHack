# Как работает dev server и HMR в Vite?

> [!NOTE]
> Vite dev server отдает модули браузеру по запросу и быстро обновляет измененные части приложения через HMR. Это ускоряет разработку по сравнению с полной пересборкой bundle на каждое изменение.

## Запуск

```bash
npm run dev
```

Обычно в `package.json`:

```json
{
  "scripts": {
    "dev": "vite"
  }
}
```

## Что делает dev server?

```txt
Browser requests /src/main.ts
Vite transforms module
Browser imports dependencies
Vite transforms only needed files
```

В dev режиме Vite активно использует native ES modules браузера.

## HMR

HMR = Hot Module Replacement. Когда меняется компонент:

```txt
save App.vue
 -> Vite detects change
 -> sends update to browser
 -> Vue updates component
 -> app state often stays alive
```

Это быстрее и приятнее, чем полный reload.

## Когда происходит full reload?

Full reload может случиться, если:

- изменился файл, который нельзя hot-replace;
- изменилась config;
- сломался module graph;
- plugin не умеет HMR для такого изменения.

## Dev server options

```typescript
export default defineConfig({
  server: {
    port: 5173,
    open: true,
    proxy: {
      "/api": "http://localhost:3000",
    },
  },
});
```

Proxy удобен, чтобы frontend ходил на `/api`, а Vite перенаправлял запросы на backend.

## Мини-шпаргалка

- `npm run dev` запускает Vite dev server.
- Vite в dev отдает ESM modules.
- HMR обновляет части приложения без full reload.
- Не все изменения можно hot-replace.
- `server.proxy` помогает связать frontend и backend в dev.
