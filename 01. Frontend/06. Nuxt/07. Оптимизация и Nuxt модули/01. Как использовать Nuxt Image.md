# Как использовать Nuxt Image?

> [!NOTE]
> Nuxt Image оптимизирует изображения через компоненты `<NuxtImg>` и `<NuxtPicture>`. Он может менять размер, формат, quality, provider, генерировать responsive `srcset` и работать с local/remote images.

## Установка

```bash
npx nuxi@latest module add image
```

Или вручную:

```ts
export default defineNuxtConfig({
  modules: ['@nuxt/image'],
});
```

## `<NuxtImg>`

```vue
<template>
  <NuxtImg
    src="/images/product.jpg"
    alt="Механическая клавиатура"
    width="600"
    height="400"
    loading="lazy"
  />
</template>
```

`<NuxtImg>` является drop-in replacement для `<img>`, но добавляет оптимизацию.

## Responsive sizes

```vue
<NuxtImg
  src="/images/hero.jpg"
  alt="Nuxt приложение"
  sizes="100vw sm:600px md:900px lg:1200px"
/>
```

Nuxt Image может сгенерировать responsive sizes/srcset.

## Remote domains

Для внешних изображений нужно разрешить domains:

```ts
export default defineNuxtConfig({
  image: {
    domains: ['images.example.com'],
  },
});
```

## Что важно для performance?

- задавать `width` и `height`;
- всегда писать `alt`;
- использовать `loading="lazy"` для offscreen images;
- не грузить огромные изображения для маленьких карточек;
- использовать правильный provider.

## Мини-шпаргалка

- Nuxt Image оптимизирует local и remote images.
- `<NuxtImg>` заменяет `<img>`.
- `<NuxtPicture>` полезен для art direction/formats.
- Для remote images настрой `domains`.
- `alt`, `width`, `height`, `sizes`, `loading` важны.
