# Как использовать useAnimate, Motion Values и useReducedMotion?

> [!NOTE]
> Кроме декларативных props, `motion-v` дает composables: `useAnimate` для ручных scoped animations, Motion Values для анимаций вне Vue render cycle и `useReducedMotion` для адаптации интерфейса к системной настройке reduced motion.

## useAnimate

`useAnimate` возвращает `scope` и `animate`. Selectors внутри `animate` ограничены элементом, на который поставлен `ref="scope"`.

```vue
<script setup lang="ts">
import { onMounted } from "vue";
import { useAnimate } from "motion-v";

const [scope, animate] = useAnimate();

onMounted(() => {
  animate("li", { opacity: 1, y: 0 }, { delay: 0.05 });
});
</script>

<template>
  <ul ref="scope">
    <li
      v-for="item in items"
      :key="item.id"
      :style="{ opacity: 0, transform: 'translateY(12px)' }"
    >
      {{ item.title }}
    </li>
  </ul>
</template>
```

Если component удалится, анимации, запущенные через scoped `animate`, будут очищены автоматически.

## Когда нужен useAnimate?

- timeline-like sequences;
- анимация нескольких child elements;
- ручной запуск после API response;
- интеграция со сторонним DOM;
- сложная анимация, которую неудобно выразить через props.

## Motion Values

Motion Values позволяют обновлять animated values вне Vue render cycle.

```vue
<script setup lang="ts">
import { onMounted } from "vue";
import { motion, useMotionValue } from "motion-v";

const x = useMotionValue(0);

onMounted(() => {
  x.set(120);
});
</script>

<template>
  <motion.div :style="{ x }" />
</template>
```

Это полезно для performance-sensitive values: drag, scroll, pointer movement.

## useReducedMotion

```vue
<script setup lang="ts">
import { computed } from "vue";
import { motion, useReducedMotion } from "motion-v";

const shouldReduceMotion = useReducedMotion();

const initial = computed(() =>
  shouldReduceMotion.value
    ? { opacity: 0 }
    : { opacity: 0, y: 32 },
);
</script>

<template>
  <motion.div
    :initial="initial"
    :animate="{ opacity: 1, y: 0 }"
  />
</template>
```

Если пользователь включил reduced motion в системе, лучше убрать parallax, большие перемещения и autoplay-анимации.

## Мини-шпаргалка

- `useAnimate` дает scoped manual animations.
- `scope` нужно повесить на DOM/SVG/motion element.
- Motion Values обновляются вне Vue render cycle.
- `useMotionValue` полезен для performance-sensitive styles.
- `useReducedMotion` уважает системную настройку пользователя.
- Для accessibility лучше заменять движение opacity/fade эффектами.
