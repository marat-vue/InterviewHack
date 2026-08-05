# Как использовать useHead и useSeoMeta?

> [!NOTE]
> `useHead` управляет содержимым `<head>`, а `useSeoMeta` дает типобезопасный способ задавать SEO meta tags. Для обычных страниц чаще используют `useSeoMeta`, а `useHead` оставляют для link, script, html attrs и нестандартных head-настроек.

## `useSeoMeta`

```vue
<script setup lang="ts">
useSeoMeta({
  title: 'Каталог товаров',
  description: 'Купить товары для frontend-разработчиков.',
  ogTitle: 'Каталог товаров',
  ogDescription: 'Подборка полезных товаров.',
  ogImage: '/og/catalog.png',
  twitterCard: 'summary_large_image',
});
</script>
```

`useSeoMeta` помогает избежать ошибок вроде неправильного `name`/`property`.

## `useHead`

```ts
useHead({
  htmlAttrs: {
    lang: 'ru',
  },
  link: [
    {
      rel: 'canonical',
      href: 'https://example.com/products',
    },
  ],
});
```

## Dynamic meta

```vue
<script setup lang="ts">
const route = useRoute();
const { data: post } = await useFetch(`/api/posts/${route.params.slug}`);

useSeoMeta({
  title: () => post.value?.title,
  description: () => post.value?.description,
  ogImage: () => post.value?.cover,
});
</script>
```

## `titleTemplate`

В `nuxt.config.ts`:

```ts
export default defineNuxtConfig({
  app: {
    head: {
      titleTemplate: '%s · My Site',
    },
  },
});
```

Страница:

```ts
useSeoMeta({
  title: 'Блог',
});
```

Итог:

```text
Блог · My Site
```

## Мини-шпаргалка

- `useSeoMeta` - основной composable для SEO meta.
- `useHead` - общий контроль над head.
- `titleTemplate` удобно задавать глобально.
- Canonical задается через `link`.
- Dynamic meta можно строить от загруженных данных.
