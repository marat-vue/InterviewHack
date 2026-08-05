# Что такое SSR в Nuxt?

> [!NOTE]
> SSR, Server-Side Rendering, означает, что Nuxt рендерит Vue-страницу на сервере и отправляет браузеру готовый HTML. Это улучшает initial load, SEO и доступность, а затем browser гидрирует страницу и делает ее интерактивной.

## Как работает SSR?

Упрощенный flow:

```text
Browser запрашивает /products
Nuxt server выполняет page setup и data fetching
Nuxt рендерит Vue в HTML
Browser получает готовый HTML
Browser загружает JS
Vue hydration подключает интерактивность
```

## Пример

```vue
<script setup lang="ts">
const { data: products } = await useFetch('/api/products');
</script>

<template>
  <ProductCard
    v-for="product in products"
    :key="product.id"
    :product="product"
  />
</template>
```

При SSR Nuxt может получить products на сервере и отправить HTML со списком товаров.

## Почему SSR полезен?

- поисковики сразу видят HTML;
- пользователь быстрее видит контент;
- меньше работы на слабых устройствах до первого отображения;
- лучше accessibility на initial load;
- данные можно безопасно получать на сервере.

## Минусы SSR

- нужен server runtime;
- код должен быть SSR-safe;
- нельзя без проверки обращаться к `window` и `document`;
- можно получить hydration mismatch;
- server должен выдерживать requests.

## Мини-шпаргалка

- SSR рендерит HTML на сервере.
- Nuxt SSR включен по умолчанию.
- После SSR происходит hydration.
- SSR полезен для SEO и first content.
- Browser-only APIs требуют `.client` или проверки окружения.
