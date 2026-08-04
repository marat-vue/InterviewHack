# Что такое emit?

> [!NOTE] Коротко
> `emit` во Vue - способ дочернего компонента отправить событие родителю. Так ребенок сообщает о действии, а родитель сам решает, как изменить состояние.

## Вопрос

Что такое `emit` во Vue?

## Базовый пример

```vue
<!-- ChildCounter.vue -->
<script setup>
const emit = defineEmits<{ increment: [] }>();
</script>

<template>
  <button @click="emit('increment')">+</button>
</template>
```

```vue
<!-- Parent.vue -->
<script setup>
import { ref } from "vue";

const count = ref(0);
</script>

<template>
  <ChildCounter @increment="count++" />
  <p>{{ count }}</p>
</template>
```

Ребенок не меняет `count` напрямую. Он только сообщает: "произошло событие".

## С payload

Событие может передавать данные.

```vue
<script setup>
const emit = defineEmits<{
  select: [id: number];
}>();
</script>

<template>
  <button @click="emit('select', 42)">Выбрать</button>
</template>
```

```vue
<UserItem @select="selectedId = $event" />
```

## Emit и однонаправленный поток

Props идут сверху вниз, events идут снизу вверх. Это сохраняет понятный источник состояния.

## Мини-шпаргалка

- `emit` отправляет событие из ребенка родителю.
- В `<script setup>` используют `defineEmits`.
- Событие может передавать payload.
- Для изменения props отправляй событие, а не мутируй prop.
