# Как работает lazy hydration в Nuxt?

> [!NOTE]
> Lazy hydration откладывает подключение интерактивности к компоненту до нужного момента: когда он станет видимым, браузер освободится или пользователь начнет взаимодействовать. Это уменьшает initial JavaScript work.

## Зачем нужна lazy hydration?

SSR может отдать HTML быстро, но hydration тяжелых компонентов может нагружать main thread.

Примеры тяжелых компонентов:

- charts;
- carousels;
- maps;
- comments widgets;
- video embeds;
- complex filters;
- recommendation blocks.

## Lazy component

Nuxt поддерживает lazy loading components через prefix:

```vue
<LazyProductRecommendations />
```

Но lazy loading component не всегда то же самое, что lazy hydration. Lazy loading откладывает загрузку кода, hydration strategies откладывают интерактивность.

## `defineLazyHydrationComponent`

Nuxt предоставляет utility для lazy hydration strategies.

Идея:

```ts
const LazyChart = defineLazyHydrationComponent(
  'visible',
  () => import('~/components/HeavyChart.vue'),
);
```

Компонент можно гидрировать, когда он станет видимым.

## Когда использовать?

Используй для:

- below-the-fold components;
- expensive widgets;
- secondary UI;
- components not needed immediately.

Не используй для:

- first-screen critical controls;
- auth forms;
- navigation;
- primary CTA.

## Мини-шпаргалка

- Lazy hydration откладывает интерактивность.
- Это снижает initial JS work.
- Подходит для тяжелых below-the-fold components.
- Не откладывай критичный UI.
- Проверяй эффект через performance tools.

