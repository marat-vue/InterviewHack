# Как обновлять и очищать Nuxt data?

> [!NOTE]
> Nuxt предоставляет utilities для работы с закэшированными async data: `refreshNuxtData`, `clearNuxtData`, `useNuxtData`. Они помогают обновлять данные после mutation, переиспользовать cache и делать optimistic UI.

## `refreshNuxtData`

Обновить все async data:

```ts
await refreshNuxtData();
```

Обновить конкретный key:

```ts
await refreshNuxtData('products');
```

Пример после создания товара:

```ts
await $fetch('/api/products', {
  method: 'POST',
  body: form.value,
});

await refreshNuxtData('products');
```

## `clearNuxtData`

```ts
clearNuxtData('profile');
```

Полезно при logout:

```ts
async function logout() {
  await $fetch('/api/auth/logout', { method: 'POST' });
  clearNuxtData();
  await navigateTo('/login');
}
```

## `useNuxtData`

```ts
const { data: cachedProducts } = useNuxtData('products');
```

Можно получить текущее кэшированное значение по key.

## Почему key важен?

Если key нестабилен или неочевиден, сложно обновлять конкретные данные.

Плохо:

```ts
useAsyncData(() => $fetch('/api/products'));
```

Лучше:

```ts
useAsyncData('products', () => $fetch('/api/products'));
```

## Мини-шпаргалка

- `refreshNuxtData(key)` перезагружает async data.
- `clearNuxtData(key)` очищает cache.
- `useNuxtData(key)` читает cached data.
- Stable keys важны для управления cache.
- После mutation часто нужен refresh конкретного key.
