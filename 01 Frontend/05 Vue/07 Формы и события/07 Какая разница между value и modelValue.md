# Какая разница между value и modelValue?

> [!NOTE]
> `value` - обычный HTML-атрибут или prop, а `modelValue` во Vue 3 - стандартный prop для компонентного `v-model`.

## Вопрос

Какая разница между `value` и `modelValue`?

## value в обычном input

```vue
<input :value="email" @input="email = $event.target.value" />
```

У HTML input есть свойство `value`. Оно хранит текущее значение поля.

## modelValue в компоненте

Во Vue 3 `v-model` на компоненте по умолчанию разворачивается в `modelValue` и `update:modelValue`.

```vue
<BaseInput v-model="email" />
```

Эквивалент:

```vue
<BaseInput
  :model-value="email"
  @update:model-value="email = $event"
/>
```

## Как написать компонент

```vue
<script setup>
defineProps<{ modelValue: string }>();
const emit = defineEmits<{ "update:modelValue": [value: string] }>();
</script>

<template>
  <input
    :value="modelValue"
    @input="emit('update:modelValue', ($event.target as HTMLInputElement).value)"
  />
</template>
```

Внутри компонента `modelValue` приходит как prop, а обновление отправляется событием.

## Почему не просто value

`modelValue` делает контракт `v-model` явным и не конфликтует с обычным HTML `value`. Также Vue 3 поддерживает несколько моделей на одном компоненте.

```vue
<UserName v-model:first-name="firstName" v-model:last-name="lastName" />
```

## Мини-шпаргалка

- `value` - обычное значение input.
- `modelValue` - стандартный prop для Vue 3 component `v-model`.
- Обновление: `update:modelValue`.
- Внутри кастомного input часто связывают `modelValue` с HTML `value`.
