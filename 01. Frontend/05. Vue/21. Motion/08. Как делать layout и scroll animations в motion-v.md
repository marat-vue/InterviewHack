# Как делать layout и scroll animations в motion-v?

> [!NOTE]
> Motion умеет анимировать изменения layout через prop `layout`, shared layout через `layoutId`, scroll-triggered animation через `whileInView` и scroll-linked animation через `useScroll`, `useSpring`, `useTransform`.

## Layout animation

```vue
<motion.div layout class="rounded-lg bg-white p-4 shadow">
  <button @click="expanded = !expanded">Toggle</button>

  <p v-if="expanded">
    Дополнительный текст
  </p>
</motion.div>
```

Когда размер блока изменится, Motion плавно анимирует layout change.

## Shared layout через layoutId

```vue
<template>
  <nav class="flex gap-4">
    <button
      v-for="tab in tabs"
      :key="tab.id"
      class="relative px-3 py-2"
      @click="activeTab = tab.id"
    >
      {{ tab.title }}

      <motion.div
        v-if="activeTab === tab.id"
        layoutId="active-tab-underline"
        class="absolute inset-x-0 bottom-0 h-0.5 bg-blue-600"
      />
    </button>
  </nav>
</template>
```

Один и тот же `layoutId` позволяет визуально перенести элемент между местами.

## Scroll-triggered animation

```vue
<motion.section
  :initial="{ opacity: 0, y: 32 }"
  :whileInView="{ opacity: 1, y: 0 }"
  :inViewOptions="{ once: true }"
  :transition="{ duration: 0.4 }"
>
  Pricing
</motion.section>
```

`whileInView` запускает анимацию при попадании элемента в viewport.

## Scroll-linked animation

```vue
<script setup lang="ts">
import { motion, useScroll, useSpring } from "motion-v";

const { scrollYProgress } = useScroll();
const scaleX = useSpring(scrollYProgress, {
  stiffness: 100,
  damping: 30,
  restDelta: 0.001,
});
</script>

<template>
  <motion.div
    class="fixed left-0 top-0 h-1 origin-left bg-blue-600"
    :style="{ scaleX }"
  />
</template>
```

Так получается progress bar, связанный со scroll страницы.

## useTransform

```typescript
const opacity = useTransform(scrollYProgress, [0, 0.3], [0, 1]);
```

`useTransform` превращает один motion value в другой: progress в opacity, y, scale, color и так далее.

## Мини-шпаргалка

- `layout` анимирует изменение размеров/позиции.
- `layoutId` нужен для shared layout animation.
- `whileInView` запускает animation при входе в viewport.
- `inViewOptions.once` запускает reveal один раз.
- `useScroll` дает scroll motion values.
- `useSpring` сглаживает motion value.
- `useTransform` мапит progress в другое значение.
