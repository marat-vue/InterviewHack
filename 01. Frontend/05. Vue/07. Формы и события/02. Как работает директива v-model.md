# Как работает директива v-model?

> [!NOTE]
> `v-model` синтаксически объединяет привязку значения и обработку события изменения. На input это value/input, на компоненте - `modelValue/update:modelValue`.

## Вопрос

Как работает директива `v-model`?

## На input

```vue
<script setup>
import { ref } from "vue";

const email = ref("");
</script>

<template>
  <input v-model="email" />
</template>
```

При вводе текста `email` обновляется.

## Эквивалентная ручная запись

```vue
<input
  :value="email"
  @input="email = ($event.target as HTMLInputElement).value"
/>
```

`v-model` просто делает эту связку компактной и учитывает особенности разных элементов формы.

## Checkbox

```vue
<input v-model="accepted" type="checkbox" />
```

Для checkbox Vue связывает checked-состояние.

## Select

```vue
<select v-model="role">
  <option value="admin">Admin</option>
  <option value="user">User</option>
</select>
```

## На компоненте

```vue
<BaseInput v-model="email" />
```

Разворачивается в:

```vue
<BaseInput
  :model-value="email"
  @update:model-value="email = $event"
/>
```

## Мини-шпаргалка

- `v-model` = value binding + update event.
- Для input обычно работает через `input`.
- Для checkbox использует checked.
- Для компонента во Vue 3: `modelValue` и `update:modelValue`.
- Можно добавлять модификаторы `.lazy`, `.trim`, `.number`.
