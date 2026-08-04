# Как использовать variants в Motion for Vue?

> [!NOTE]
> Variants позволяют назвать состояния анимации: `hidden`, `visible`, `active`, `disabled`. Вместо больших объектов в template компонент переключает понятные labels, а animation config хранится рядом в script.

## Без variants

```vue
<motion.div
  :initial="{ opacity: 0, y: 20 }"
  :animate="{ opacity: 1, y: 0 }"
/>
```

Для одного элемента это нормально. Но для сложного компонента template быстро становится шумным.

## С variants

```vue
<script setup lang="ts">
import { motion } from "motion-v";

const cardVariants = {
  hidden: {
    opacity: 0,
    y: 20,
  },
  visible: {
    opacity: 1,
    y: 0,
    transition: { duration: 0.3 },
  },
};
</script>

<template>
  <motion.article
    :variants="cardVariants"
    initial="hidden"
    animate="visible"
  />
</template>
```

Теперь template читает смысл, а не детали.

## Reactive variants

```vue
<motion.div
  :variants="{
    active: { scale: 1, opacity: 1 },
    inactive: { scale: 0.96, opacity: 0.6 },
  }"
  :animate="isActive ? 'active' : 'inactive'"
/>
```

`animate` может быть строкой variant name.

## Parent и children

Variants удобны для списков:

```vue
<script setup lang="ts">
const list = {
  hidden: { opacity: 0 },
  visible: {
    opacity: 1,
    transition: {
      staggerChildren: 0.06,
    },
  },
};

const item = {
  hidden: { opacity: 0, y: 12 },
  visible: { opacity: 1, y: 0 },
};
</script>

<template>
  <motion.ul :variants="list" initial="hidden" animate="visible">
    <motion.li
      v-for="product in products"
      :key="product.id"
      :variants="item"
    >
      {{ product.title }}
    </motion.li>
  </motion.ul>
</template>
```

Так можно сделать красивое каскадное появление списка.

## Когда использовать variants?

Используй variants, если:

- states повторяются;
- анимация большая;
- есть parent-child orchestration;
- нужно переключать named states;
- template стал нечитаемым.

## Мини-шпаргалка

- Variants называют состояния анимации.
- `initial`, `animate`, `exit`, gestures могут ссылаться на variant name.
- Variants разгружают template.
- `staggerChildren` помогает анимировать списки.
- Для одного простого элемента variants не обязательны.
