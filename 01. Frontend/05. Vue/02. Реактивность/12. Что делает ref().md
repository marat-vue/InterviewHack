# Что делает ref()?

> [!NOTE]
> `ref()` создает реактивную обертку над значением. В JavaScript-коде значение читается и меняется через `.value`, а в шаблоне Vue разворачивает его автоматически.

## Вопрос

Что делает `ref()`?

## Базовый пример

```vue
<script setup>
import { ref } from "vue";

const count = ref(0);

function increment() {
  count.value++;
}
</script>

<template>
  <button @click="increment">{{ count }}</button>
</template>
```

В `<script setup>` нужно `count.value`, а в template можно писать просто `count`.

## Ref для разных значений

```typescript
const name = ref("Анна");
const isOpen = ref(false);
const user = ref<User | null>(null);
```

`ref` подходит и для примитивов, и для объектов.

## Замена значения целиком

```typescript
const user = ref({ name: "Анна" });

user.value = { name: "Мария" };
```

Это удобно, когда состояние нужно полностью заменить.

## Ref для DOM

```vue
<script setup>
import { ref, onMounted } from "vue";

const inputRef = ref<HTMLInputElement | null>(null);

onMounted(() => {
  inputRef.value?.focus();
});
</script>

<template>
  <input ref="inputRef" />
</template>
```

## Мини-шпаргалка

- `ref(value)` создает реактивное значение.
- В script доступ через `.value`.
- В template ref разворачивается автоматически.
- Хорош для примитивов, nullable-значений и DOM refs.
