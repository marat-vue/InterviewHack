# Как использовать motion component, initial, animate и transition?

> [!NOTE]
> `<motion.*>` component выглядит как обычный HTML/SVG элемент, но принимает animation props. Главные props: `initial` задает стартовое состояние, `animate` задает целевое состояние, `transition` управляет длительностью, easing и spring.

## Базовый пример

```vue
<script setup lang="ts">
import { motion } from "motion-v";
</script>

<template>
  <motion.div
    class="rounded-lg bg-blue-600 p-4 text-white"
    :initial="{ opacity: 0, y: 24 }"
    :animate="{ opacity: 1, y: 0 }"
  >
    Animated card
  </motion.div>
</template>
```

`initial` - откуда начинается анимация. `animate` - куда элемент приходит.

## Transition

```vue
<motion.div
  :initial="{ opacity: 0, scale: 0.9 }"
  :animate="{ opacity: 1, scale: 1 }"
  :transition="{ duration: 0.35, ease: 'easeOut' }"
/>
```

`duration` задается в секундах.

## Spring transition

```vue
<motion.button
  :whilePress="{ scale: 0.96 }"
  :transition="{ type: 'spring', stiffness: 400, damping: 24 }"
>
  Нажми
</motion.button>
```

Spring часто выглядит живее для UI-interactions: кнопки, cards, draggable элементы.

## Reactive animate

```vue
<script setup lang="ts">
import { ref } from "vue";
import { motion } from "motion-v";

const isOpen = ref(false);
</script>

<template>
  <button @click="isOpen = !isOpen">Toggle</button>

  <motion.div
    :animate="{
      height: isOpen ? 200 : 80,
      opacity: isOpen ? 1 : 0.7,
    }"
  />
</template>
```

Когда Vue state меняется, `animate` получает новые значения, и Motion анимирует переход.

## Отключение initial animation

```vue
<motion.div :initial="false" :animate="{ opacity: 1 }" />
```

`initial="false"` полезен, если компонент не должен проигрывать enter-анимацию при первом render.

## Какие свойства можно анимировать?

Частые свойства:

- `opacity`;
- `x`, `y`;
- `scale`;
- `rotate`;
- `width`, `height`;
- `backgroundColor`;
- `borderRadius`;
- SVG attributes;
- CSS variables, если они числовые/анимируемые.

Для производительности чаще предпочитают `transform` и `opacity`.

## Мини-шпаргалка

- `<motion.div>` - анимированный `div`.
- `initial` задает старт.
- `animate` задает цель.
- `transition` настраивает движение.
- `animate` может зависеть от Vue state.
- `initial={false}` отключает стартовую анимацию.
- `opacity` и transforms обычно самые безопасные для performance.
