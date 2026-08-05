# Как использовать useAsyncData?

> [!NOTE]
> `useAsyncData` загружает любые async-данные в Nuxt context и сохраняет результат в payload. Он полезен, когда источник данных не является простым HTTP endpoint или когда нужна кастомная функция загрузки.

## Базовый пример

```ts
const { data: post, error } = await useAsyncData('post:nuxt-ssr', () => {
  return queryContent('/blog/nuxt-ssr').findOne();
});
```

Первый аргумент - key. Он нужен Nuxt для кэша/payload.

## С repository

```ts
const { $api } = useNuxtApp();

const { data: products } = await useAsyncData('products', () => {
  return $api('/products');
});
```

Это лучше, чем просто `$api('/products')` в setup, потому что Nuxt сможет передать данные клиенту через payload.

## Watch

```ts
const category = ref('books');

const { data } = await useAsyncData(
  'products-by-category',
  () => $fetch('/api/products', {
    query: { category: category.value },
  }),
  {
    watch: [category],
  },
);
```

## Transform и pick

```ts
const { data } = await useAsyncData(
  'profile',
  () => $fetch('/api/profile'),
  {
    transform: (profile) => ({
      name: profile.name,
      avatar: profile.avatar,
    }),
  },
);
```

## Когда использовать?

- custom API client;
- database/content query;
- объединение нескольких requests;
- transform данных перед payload;
- работа не только с HTTP.

## Мини-шпаргалка

- `useAsyncData` подходит для любой async-функции.
- Key должен быть стабильным и понятным.
- Результат попадает в Nuxt payload.
- Для HTTP проще начать с `useFetch`.
- Для custom `$api` часто используют `useAsyncData`.
