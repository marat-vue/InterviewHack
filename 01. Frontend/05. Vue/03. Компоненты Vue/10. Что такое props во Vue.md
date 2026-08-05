# Что такое props во Vue?

> [!NOTE]
> Props во Vue - входные данные компонента. Родитель передает их ребенку, а ребенок использует их для отображения или вычислений.

## Вопрос

Что такое props во Vue?

## Базовый пример

```vue
<!-- Parent.vue -->
<template>
  <UserCard :user="user" />
</template>
```

```vue
<!-- UserCard.vue -->
<script setup>
type User = {
  id: number;
  name: string;
};

defineProps<{
  user: User;
}>();
</script>

<template>
  <h2>{{ user.name }}</h2>
</template>
```

## Props как контракт

Props описывают, что компонент ожидает получить от родителя. Хорошее имя prop делает компонент проще использовать.

```vue
<BaseButton :disabled="isSaving" variant="primary">
  Сохранить
</BaseButton>
```

## Значения по умолчанию

```vue
<script setup>
const props = withDefaults(
  defineProps<{
    size?: "sm" | "md" | "lg";
  }>(),
  {
    size: "md",
  }
);
</script>
```

## Props не изменяют напрямую

Если нужно изменить значение, ребенок отправляет событие, а родитель обновляет состояние.

## Мини-шпаргалка

- Props - вход компонента.
- Родитель передает props через атрибуты.
- Динамические значения передают через `:prop`.
- В дочернем компоненте props readonly.
- Для обратной связи нужен emit.
