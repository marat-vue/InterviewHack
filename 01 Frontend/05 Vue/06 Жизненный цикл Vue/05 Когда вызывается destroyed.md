# Когда вызывается destroyed?

> [!NOTE]
> `destroyed` - хук Vue 2, который вызывался после уничтожения компонента. Во Vue 3 его заменили на `unmounted`, а перед ним есть `beforeUnmount`.

## Вопрос

Когда вызывается `destroyed`?

## Vue 2

```javascript
export default {
  destroyed() {
    console.log("Компонент уничтожен");
  },
};
```

В Vue 2 `destroyed` вызывался после удаления компонента и очистки его реактивных связей.

## Vue 3

Во Vue 3 используется `unmounted`.

```javascript
export default {
  unmounted() {
    console.log("Компонент удален");
  },
};
```

В Composition API:

```vue
<script setup>
import { onUnmounted } from "vue";

onUnmounted(() => {
  console.log("Очистка после компонента");
});
</script>
```

## Что очищать

```typescript
onMounted(() => {
  window.addEventListener("resize", onResize);
});

onUnmounted(() => {
  window.removeEventListener("resize", onResize);
});
```

В `unmounted` очищают таймеры, подписки, listeners, соединения и экземпляры сторонних библиотек.

## Мини-шпаргалка

- `destroyed` - название из Vue 2.
- Во Vue 3 актуальный хук - `unmounted`.
- В Composition API - `onUnmounted`.
- Главная задача - cleanup side effects.
