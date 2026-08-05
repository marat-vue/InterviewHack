# Можно ли использовать ref внутри композиционных хуков?

> [!NOTE]
> Да, `ref` можно использовать внутри composable-функций и lifecycle hooks. Главное - создавать и регистрировать реактивную логику синхронно во время `setup`.

## Вопрос

Можно ли использовать `ref` внутри композиционных хуков?

## Ref внутри composable

```typescript
import { ref } from "vue";

export function useCounter() {
  const count = ref(0);
  const increment = () => count.value++;

  return { count, increment };
}
```

Такой composable можно вызвать в компоненте.

```vue
<script setup>
const { count, increment } = useCounter();
</script>
```

## Ref внутри lifecycle hook

```vue
<script setup>
import { onMounted, ref } from "vue";

const width = ref(0);

onMounted(() => {
  width.value = window.innerWidth;
});
</script>
```

Менять `ref` внутри hook можно.

## Важное ограничение

Регистрировать hooks нужно синхронно.

```typescript
onMounted(() => {
  console.log("ok");
});
```

Не делай регистрацию hook внутри асинхронного callback.

## Cleanup

```typescript
export function useWindowWidth() {
  const width = ref(window.innerWidth);

  const update = () => {
    width.value = window.innerWidth;
  };

  onMounted(() => window.addEventListener("resize", update));
  onUnmounted(() => window.removeEventListener("resize", update));

  return { width };
}
```

## Мини-шпаргалка

- `ref` можно создавать в composables.
- `ref.value` можно менять внутри lifecycle hooks.
- Hooks регистрируются синхронно во время `setup`.
- Side effects нужно очищать в `onUnmounted`.
