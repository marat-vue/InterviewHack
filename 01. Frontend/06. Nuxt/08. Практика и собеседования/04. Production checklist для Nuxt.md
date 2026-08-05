# Production checklist для Nuxt

> [!NOTE]
> Перед production Nuxt-приложение нужно проверить по нескольким направлениям: rendering modes, routeRules, SEO, runtime config, server API, images/fonts/scripts, security headers, error pages, monitoring и deployment output.

## Rendering

- SSR/SSG/ISR/CSR выбраны осознанно.
- `routeRules` не кэшируют приватный HTML.
- Нет hydration mismatch warnings.
- Browser-only libraries вынесены в `.client` или `<ClientOnly>`.

## Data и config

- `useFetch/useAsyncData` используются для initial SSR data.
- `$fetch` не вызывает double fetch там, где нужен payload.
- Secrets не лежат в `runtimeConfig.public`.
- Environment variables настроены для production.

## SEO

- Уникальные title/description.
- Canonical корректный.
- Sitemap отдается и содержит нужные URL.
- Robots не блокирует production.
- 404 возвращает 404.
- OG images работают.
- Structured data валидна.

## Performance

- Изображения через Nuxt Image.
- Шрифты оптимизированы.
- Third-party scripts контролируются.
- Lazy hydration применена только к некритичному UI.
- Lighthouse/Web Vitals проверены.

## Security и server

- Cookies имеют нужные flags.
- Security headers настроены.
- API routes валидируют input.
- Ошибки не раскрывают secrets.
- Logs и error monitoring подключены.

## Мини-шпаргалка

- Проверь rendering, SEO, data, security, performance.
- `nuxt build` и `nuxt preview` должны проходить без неожиданных warnings.
- Production env не должен совпадать с local defaults.
- Sitemap/robots/OG лучше проверить реальными URL.
- Monitoring нужен до первого инцидента, а не после.
