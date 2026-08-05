# Что такое Pinia?

> [!NOTE]
> Pinia - официальный state manager для Vue. Она позволяет создавать stores с состоянием, getters и actions и использовать их в разных компонентах.

## Вопрос

Что такое Pinia?

## Базовый store

```typescript
import { defineStore } from "pinia";

export const useCounterStore = defineStore("counter", {
  state: () => ({
    count: 0,
  }),
  getters: {
    doubled: (state) => state.count * 2,
  },
  actions: {
    increment() {
      this.count++;
    },
  },
});
```

## Использование

```vue
<script setup>
import { useCounterStore } from "@/stores/counter";

const counter = useCounterStore();
</script>

<template>
  <button @click="counter.increment">
    {{ counter.doubled }}
  </button>
</template>
```

## Setup store

Pinia также поддерживает store в стиле Composition API.

```typescript
export const useCounterStore = defineStore("counter", () => {
  const count = ref(0);
  const doubled = computed(() => count.value * 2);
  const increment = () => count.value++;

  return { count, doubled, increment };
});
```

## Что хранить в Pinia

Текущего пользователя, корзину, права доступа, настройки, общий кэш данных, состояние, которое нужно разным независимым экранам.

## Мини-шпаргалка

- Pinia - современный store для Vue.
- Store создается через `defineStore`.
- Есть state, getters и actions.
- Можно писать options store или setup store.
- Не заменяет локальный state для мелких UI-деталей.
- Подробный практический блок: [[01 Как подключить Pinia к Vue проекту]].
