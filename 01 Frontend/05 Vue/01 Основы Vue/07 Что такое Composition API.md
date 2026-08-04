# Что такое Composition API?

> [!NOTE] Коротко
> Composition API - стиль Vue 3, где логика компонента собирается через функции `ref`, `reactive`, `computed`, `watch` и lifecycle hooks внутри `setup` или `<script setup>`.

## Вопрос

Что такое Composition API?

## Базовый пример

```vue
<script setup>
import { computed, ref } from "vue";

const count = ref(0);
const doubled = computed(() => count.value * 2);

function increment() {
  count.value++;
}
</script>

<template>
  <button @click="increment">{{ doubled }}</button>
</template>
```

## Главная идея

Composition API группирует код по смыслу, а не по опциям. Логику счетчика можно держать рядом: состояние, computed и методы.

## Composables

Повторяемую логику можно вынести в функцию.

```typescript
import { ref } from "vue";

export function useCounter() {
  const count = ref(0);
  const increment = () => count.value++;

  return { count, increment };
}
```

## Когда удобен

Composition API особенно полезен в больших компонентах, при переиспользовании логики, с TypeScript и в сложных сценариях реактивности.

## Мини-шпаргалка

- Основа Vue 3 для сложной логики.
- Часто используется через `<script setup>`.
- `ref` и `reactive` создают состояние.
- Composables позволяют переиспользовать логику.
