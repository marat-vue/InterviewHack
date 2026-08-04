# Что такое lazy data fetching?

> [!NOTE]
> Lazy data fetching позволяет не блокировать navigation ожиданием данных. В Nuxt для этого используют `useLazyFetch`, `useLazyAsyncData` или option `lazy: true`.

## Обычный `useFetch`

По умолчанию `useFetch` может блокировать переход, пока данные не загружены:

```ts
const { data } = await useFetch('/api/products');
```

Это хорошо, если страница не должна показываться без данных.

## `useLazyFetch`

```ts
const { data, status } = await useLazyFetch('/api/products');
```

Navigation может продолжиться сразу, а данные загрузятся в фоне.

В template:

```vue
<template>
  <ProductSkeleton v-if="status === 'pending'" />
  <ProductList v-else :products="data" />
</template>
```

## `lazy: true`

```ts
const { data, status } = await useFetch('/api/products', {
  lazy: true,
});
```

## Когда использовать lazy?

Используй lazy, если:

- страница может показать skeleton;
- данные не критичны для initial render;
- важно быстрее перейти на route;
- часть контента below the fold;
- запрос тяжелый.

Не используй lazy, если:

- без данных страница бессмысленна;
- SEO зависит от этих данных;
- нужно отдать полный HTML поисковику.

## Мини-шпаргалка

- Lazy data fetching не блокирует navigation.
- `useLazyFetch` - lazy-версия `useFetch`.
- `useLazyAsyncData` - lazy-версия `useAsyncData`.
- Skeleton/loading state обязателен.
- Для SEO-критичных данных lazy может быть плохим выбором.
