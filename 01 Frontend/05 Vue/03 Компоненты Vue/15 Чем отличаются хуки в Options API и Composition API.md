# Чем отличаются хуки в Options API и Composition API?

> [!NOTE]
> В Options API хуки задаются как методы объекта компонента, а в Composition API подключаются функциями `onMounted`, `onUpdated`, `onUnmounted` внутри `setup`.

## Вопрос

Чем отличаются хуки в Options API и Composition API?

## Options API

```vue
<script>
export default {
  mounted() {
    console.log("mounted");
  },
  updated() {
    console.log("updated");
  },
  unmounted() {
    console.log("unmounted");
  },
};
</script>
```

Хуки находятся на верхнем уровне объекта рядом с `data`, `methods`, `computed`.

## Composition API

```vue
<script setup>
import { onMounted, onUpdated, onUnmounted } from "vue";

onMounted(() => console.log("mounted"));
onUpdated(() => console.log("updated"));
onUnmounted(() => console.log("unmounted"));
</script>
```

Хуки можно расположить рядом с логикой, к которой они относятся.

## Таблица соответствий

| Options API | Composition API |
| --- | --- |
| `beforeMount` | `onBeforeMount` |
| `mounted` | `onMounted` |
| `beforeUpdate` | `onBeforeUpdate` |
| `updated` | `onUpdated` |
| `beforeUnmount` | `onBeforeUnmount` |
| `unmounted` | `onUnmounted` |

## Важный нюанс

В Composition API lifecycle hooks нужно вызывать синхронно во время `setup`, а не внутри `setTimeout`, `then` или обработчика события.

## Мини-шпаргалка

- Options API: хуки как методы компонента.
- Composition API: хуки как функции `on...`.
- Composition API позволяет держать lifecycle рядом с composable-логикой.
- `setup` выполняется раньше `mounted`.
