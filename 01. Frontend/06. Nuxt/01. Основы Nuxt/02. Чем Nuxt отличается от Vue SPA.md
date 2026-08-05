# Чем Nuxt отличается от Vue SPA?

> [!NOTE]
> Vue SPA обычно рендерит HTML в браузере, а Nuxt может рендерить страницу на сервере, генерировать статические страницы, смешивать режимы по маршрутам и иметь server API. Поэтому Nuxt чаще выбирают, когда важны SEO, initial load, routing и production-архитектура.

## Vue SPA

В обычном Vue SPA browser получает почти пустой HTML и JavaScript bundle:

```html
<div id="app"></div>
<script src="/assets/app.js"></script>
```

Потом JavaScript загружается, запускается Vue, получает данные и строит интерфейс.

Плюсы:

- проще deploy на static hosting;
- удобно для внутренних dashboards;
- меньше серверной инфраструктуры.

Минусы:

- хуже initial HTML для SEO;
- первый meaningful render зависит от JS;
- больше работы вручную: routing, meta, code splitting, SSR.

## Nuxt

Nuxt может сразу отдать готовый HTML:

```html
<main>
  <h1>Каталог товаров</h1>
  <article>Keyboard</article>
</main>
```

Потом browser загружает JS и гидрирует страницу.

Плюсы:

- SSR/SSG из коробки;
- лучше SEO;
- быстрее perceived initial load;
- file-based routing;
- data fetching с SSR payload;
- server API через Nitro;
- гибкий hybrid rendering.

## Когда выбрать Vue SPA?

Vue SPA подходит, если:

- приложение доступно только после login;
- SEO не важно;
- контент не должен индексироваться;
- нужен максимально простой static deploy;
- backend уже отдельно существует.

## Когда выбрать Nuxt?

Nuxt подходит, если:

- нужны индексируемые страницы;
- важен first load;
- есть публичный контент;
- нужна гибкая генерация страниц;
- хочется писать frontend и легкий backend в одном проекте;
- нужна сильная module ecosystem.

## Мини-шпаргалка

- Vue SPA рендерит UI в браузере.
- Nuxt может рендерить UI на сервере или на build-time.
- Nuxt лучше для SEO и публичного контента.
- SPA проще для закрытых внутренних приложений.
- Nuxt умеет работать и как SPA через `ssr: false`.
