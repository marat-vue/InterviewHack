# Как работает двустороннее связывание (v-model)?

> [!NOTE] Коротко
> `v-model` связывает значение формы или компонента с состоянием: состояние попадает в UI, а действия пользователя обновляют состояние.

## Вопрос

Как работает двустороннее связывание через `v-model`?

## На обычном input

```vue
<script setup>
import { ref } from "vue";

const name = ref("");
</script>

<template>
  <input v-model="name" />
  <p>Привет, {{ name }}</p>
</template>
```

`name` задает значение поля, а ввод пользователя меняет `name`.

## Что происходит под капотом

Для текстового поля `v-model` примерно соответствует связке `:value` и `@input`.

```vue
<input
  :value="name"
  @input="name = $event.target.value"
/>
```

## На компоненте

В Vue 3 стандартный `v-model` использует prop `modelValue` и событие `update:modelValue`.

```vue
<!-- Parent.vue -->
<BaseInput v-model="name" />
```

```vue
<!-- BaseInput.vue -->
<script setup>
defineProps<{ modelValue: string }>();
const emit = defineEmits<{ "update:modelValue": [value: string] }>();
</script>

<template>
  <input :value="modelValue" @input="emit('update:modelValue', $event.target.value)" />
</template>
```

## Мини-шпаргалка

- `v-model` = значение вниз + событие наверх.
- Для input обновляет state по событию ввода.
- Для компонента: `modelValue` и `update:modelValue`.
- Модификаторы вроде `.trim`, `.number`, `.lazy` меняют поведение.
