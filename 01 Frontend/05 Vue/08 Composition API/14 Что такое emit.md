# Что такое emit?

> [!NOTE]
> `emit` в Composition API отправляет событие из дочернего компонента родителю. В `<script setup>` его объявляют через `defineEmits`.

## Вопрос

Что такое `emit` в Composition API?

## Базовый пример

```vue
<script setup lang="ts">
const emit = defineEmits<{ close: [] }>();

function close() {
  emit("close");
}
</script>

<template>
  <button @click="close">Закрыть</button>
</template>
```

Родитель слушает событие:

```vue
<BaseModal @close="isOpen = false" />
```

## С payload

```vue
<script setup lang="ts">
const emit = defineEmits<{
  select: [id: number];
}>();

emit("select", 42);
</script>
```

TypeScript проверит имя события и тип payload.

## Для v-model

```typescript
const emit = defineEmits<{
  "update:modelValue": [value: string];
}>();

emit("update:modelValue", "new value");
```

## Зачем нужен emit

Emit сохраняет однонаправленный поток данных: ребенок сообщает о событии, а родитель меняет состояние.

## Мини-шпаргалка

- `defineEmits` объявляет события компонента.
- `emit("event")` отправляет событие.
- Payload можно типизировать.
- Для `v-model` событие называется `update:modelValue`.
