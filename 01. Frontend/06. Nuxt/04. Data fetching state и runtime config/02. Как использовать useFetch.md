# Как использовать useFetch?

> [!NOTE]
> `useFetch` - основной SSR-friendly composable для HTTP-запросов в Nuxt. Он возвращает reactive data, status, error, refresh и умеет передавать результат через Nuxt payload без повторного запроса на hydration.

## Базовый пример

```vue
<script setup lang="ts">
const { data: products, status, error } = await useFetch('/api/products');
</script>

<template>
  <p v-if="status === 'pending'">Загрузка...</p>
  <p v-else-if="error">Не удалось загрузить товары</p>
  <ProductCard
    v-else
    v-for="product in products"
    :key="product.id"
    :product="product"
  />
</template>
```

## POST request

```ts
const { data, error } = await useFetch('/api/orders', {
  method: 'POST',
  body: {
    productId: 1,
    quantity: 2,
  },
});
```

Для submit по кнопке часто удобнее `$fetch`, потому что это действие пользователя, а не initial SSR data.

## Query params

```ts
const page = ref(1);

const { data, refresh } = await useFetch('/api/products', {
  query: {
    page,
  },
});
```

## Transform

```ts
const { data } = await useFetch('/api/products', {
  transform: (products) => products.map((product) => ({
    ...product,
    formattedPrice: formatPrice(product.price),
  })),
});
```

## Refresh

```ts
const { data, refresh } = await useFetch('/api/profile');

async function reload() {
  await refresh();
}
```

## Мини-шпаргалка

- `useFetch` хорош для SSR HTTP-запросов.
- Возвращает `data`, `status`, `error`, `refresh`.
- Результат попадает в Nuxt payload.
- Для user action можно использовать `$fetch`.
- `query`, `body`, `method`, `headers`, `transform` покрывают частые кейсы.
