# Как получить доступ к DOM через ref?

> [!NOTE] Коротко
> Для доступа к DOM во Vue используют template ref: объявляют `ref(null)`, ставят `ref="name"` в шаблоне и обращаются к элементу после `onMounted`.

## Вопрос

Как получить доступ к DOM через `ref`?

## Базовый пример

```vue
<script setup lang="ts">
import { onMounted, ref } from "vue";

const inputRef = ref<HTMLInputElement | null>(null);

onMounted(() => {
  inputRef.value?.focus();
});
</script>

<template>
  <input ref="inputRef" />
</template>
```

До монтирования значение будет `null`.

## После v-if

Если элемент создается условно, дождись обновления DOM.

```typescript
import { nextTick, ref } from "vue";

const isOpen = ref(false);
const inputRef = ref<HTMLInputElement | null>(null);

async function open() {
  isOpen.value = true;
  await nextTick();
  inputRef.value?.focus();
}
```

## Ref на компонент

```vue
<ChildForm ref="formRef" />
```

В `<script setup>` дочерний компонент должен открыть наружу методы через `defineExpose`.

```typescript
defineExpose({
  validate,
});
```

## Когда DOM ref нужен

Фокус, измерение размеров, scroll, интеграция с внешними DOM-библиотеками. Для обычного управления UI сначала выбирай декларативные props и state.

## Мини-шпаргалка

- Template ref объявляют как `ref<HTMLElement | null>(null)`.
- DOM доступен после `onMounted`.
- После `v-if` часто нужен `nextTick`.
- Для component ref используй `defineExpose`.
