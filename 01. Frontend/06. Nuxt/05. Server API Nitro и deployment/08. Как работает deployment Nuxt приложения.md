# Как работает deployment Nuxt приложения?

> [!NOTE]
> Nuxt build создает production output через Nitro. В зависимости от режима и платформы приложение можно развернуть как Node server, serverless/edge output или статический сайт после `nuxt generate`.

## Production build

```bash
npm run build
```

Nuxt создает `.output/`:

```text
.output/
  public/
  server/
```

Preview:

```bash
npm run preview
```

## Static generation

```bash
npm run generate
```

Этот режим подходит для static hosting, если приложение можно предварительно сгенерировать.

## Nitro presets

Nitro умеет адаптировать output под разные платформы:

- Node server;
- serverless;
- edge;
- Vercel;
- Netlify;
- Cloudflare;
- другие hosting targets.

Обычно preset определяется автоматически, но его можно задавать настройками deployment.

## Что проверить перед deploy?

- environment variables;
- runtimeConfig;
- routeRules;
- SSR/SSG/ISR поведение;
- server API availability;
- image/font providers;
- sitemap/robots URL;
- security headers;
- build warnings.

## Мини-шпаргалка

- `nuxt build` создает production output.
- `.output/` - результат сборки.
- `nuxt preview` проверяет production build локально.
- `nuxt generate` создает static site.
- Nitro preset адаптирует output под hosting.
