# Для чего используется v-model?

> [!NOTE]
> `v-model` используется для двусторонней привязки данных: значение из state попадает в форму или компонент, а изменение пользователем обновляет state.

## Вопрос

Для чего используется `v-model`?

## Input

```vue
<script setup>
import { ref } from "vue";

const email = ref("");
</script>

<template>
  <input v-model="email" />
  <p>{{ email }}</p>
</template>
```

При вводе текста `email` обновляется автоматически.

## Checkbox

```vue
<script setup>
const accepted = ref(false);
</script>

<template>
  <input v-model="accepted" type="checkbox" />
</template>
```

Для checkbox `v-model` работает с checked-состоянием.

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

Во Vue 3 это разворачивается в `:modelValue` и `@update:modelValue`.

```vue
<BaseInput
  :model-value="email"
  @update:model-value="email = $event"
/>
```

## Мини-шпаргалка

- `v-model` связывает form value и state.
- Для input обновляет значение при вводе.
- Для компонента использует `modelValue` и `update:modelValue`.
- Модификаторы: `.trim`, `.number`, `.lazy`.
