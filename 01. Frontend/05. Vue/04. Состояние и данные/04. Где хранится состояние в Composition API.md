# Где хранится состояние в Composition API?

> [!NOTE]
> В Composition API состояние создают внутри `setup` или `<script setup>` через `ref`, `reactive`, `computed` и composable-функции.

## Вопрос

Где хранится состояние в Composition API?

## Через ref

```vue
<script setup>
import { ref } from "vue";

const count = ref(0);
const name = ref("Анна");
</script>

<template>
  <button @click="count++">{{ count }}</button>
  <p>{{ name }}</p>
</template>
```

`ref` подходит для примитивов, nullable-значений и значений, которые заменяются целиком.

## Через reactive

```vue
<script setup>
import { reactive } from "vue";

const form = reactive({
  email: "",
  password: "",
});
</script>
```

`reactive` удобен для объектов с несколькими связанными полями.

## Через composable

```typescript
export function useCounter() {
  const count = ref(0);
  const increment = () => count.value++;

  return { count, increment };
}
```

Composable выносит состояние и действия в переиспользуемую функцию.

## Мини-шпаргалка

- Composition API state создается в `setup`.
- `ref` - для одного значения.
- `reactive` - для объекта.
- `computed` - для производного состояния.
- Composables помогают переиспользовать stateful-логику.
