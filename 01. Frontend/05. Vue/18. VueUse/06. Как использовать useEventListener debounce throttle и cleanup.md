# Как использовать useEventListener, debounce, throttle и cleanup?

> [!NOTE]
> VueUse помогает безопасно работать с browser events и частыми вызовами. `useEventListener` автоматически снимает listener, `useDebounceFn` откладывает вызов, а `useThrottleFn` ограничивает частоту выполнения.

## useEventListener

```typescript
import { useEventListener } from "@vueuse/core";

useEventListener(window, "keydown", (event) => {
  if (event.key === "Escape") {
    closeModal();
  }
});
```

Listener будет снят при unmount компонента. Это снижает риск memory leaks.

## Event target через ref

```vue
<script setup lang="ts">
const buttonRef = ref<HTMLButtonElement | null>(null);

useEventListener(buttonRef, "click", () => {
  console.log("clicked");
});
</script>

<template>
  <button ref="buttonRef">Click</button>
</template>
```

## useDebounceFn

```typescript
const search = useDebounceFn(async (query: string) => {
  await loadProducts(query);
}, 400);
```

Debounce полезен для search input: запрос отправится после паузы.

## useThrottleFn

```typescript
const onScroll = useThrottleFn(() => {
  updateScrollPosition();
}, 100);

useEventListener(window, "scroll", onScroll);
```

Throttle полезен для scroll/resize, где события могут сыпаться десятки раз в секунду.

## Мини-шпаргалка

- `useEventListener` делает add/remove listener.
- Можно передавать `window`, `document` или element ref.
- `useDebounceFn` ждет паузу перед вызовом.
- `useThrottleFn` ограничивает частоту вызовов.
- Это особенно полезно для search, scroll, resize, keyboard events.
