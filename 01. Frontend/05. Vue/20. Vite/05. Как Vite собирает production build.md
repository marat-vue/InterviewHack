# Как Vite собирает production build?

> [!NOTE]
> Production build Vite оптимизирует приложение: собирает modules, минифицирует код, разделяет chunks, обрабатывает assets, добавляет hashes к файлам и кладет результат в `dist`.

## Команда

```bash
npm run build
```

Обычно:

```json
{
  "scripts": {
    "build": "vite build",
    "preview": "vite preview"
  }
}
```

## Что появляется после build?

```txt
dist/
  index.html
  assets/
    index-8fd91c.js
    index-a12b3.css
    logo-91ab2.svg
```

Hash в имени помогает кешированию: если файл изменился, hash тоже изменится.

## Preview

```bash
npm run preview
```

`vite preview` локально показывает production build. Это не dev server и не полноценный production server, а удобная проверка собранного приложения.

## Code splitting

Lazy routes создают отдельные chunks:

```typescript
{
  path: "/admin",
  component: () => import("@/pages/AdminPage.vue"),
}
```

Так admin page не попадет в initial chunk.

## Build options

```typescript
export default defineConfig({
  build: {
    outDir: "dist",
    sourcemap: true,
    chunkSizeWarningLimit: 1000,
  },
});
```

Sourcemaps полезны для debugging production errors, но их публикацию нужно согласовать с security/team policy.

## Мини-шпаргалка

- Build запускается через `vite build`.
- Результат обычно лежит в `dist`.
- Assets получают hashes.
- Lazy imports помогают code splitting.
- `vite preview` проверяет production build локально.
- Sourcemaps полезны, но требуют осознанного publishing.
