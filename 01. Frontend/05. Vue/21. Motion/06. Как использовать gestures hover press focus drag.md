# Как использовать gestures hover, press, focus и drag?

> [!NOTE]
> Motion расширяет обычные события Vue gesture-пропсами: `whileHover`, `whilePress`, `whileFocus`, `whileDrag`, `drag`, `dragConstraints`, `dragElastic`, `dragMomentum` и gesture events вроде `hoverStart`, `press`, `pan`.

## Hover и press

```vue
<script setup lang="ts">
import { motion } from "motion-v";
</script>

<template>
  <motion.button
    class="rounded-lg bg-blue-600 px-4 py-2 text-white"
    :whileHover="{ scale: 1.04 }"
    :whilePress="{ scale: 0.96 }"
    :transition="{ type: 'spring', stiffness: 400, damping: 24 }"
  >
    Купить
  </motion.button>
</template>
```

`whileHover` активен во время hover. `whilePress` активен во время pointer press/tap.

## Gesture events

```vue
<motion.div
  :whileHover="{ scale: 1.05 }"
  @hoverStart="() => console.log('hover start')"
  @hoverEnd="() => console.log('hover end')"
/>
```

Для press:

```vue
<motion.button
  :whilePress="{ scale: 0.95 }"
  @press="submit"
/>
```

## Focus

```vue
<motion.input
  class="rounded border px-3 py-2"
  :whileFocus="{ scale: 1.02, borderColor: '#2563eb' }"
/>
```

Focus-анимации должны помогать keyboard navigation, а не прятать outline полностью.

## Drag

```vue
<motion.div
  class="h-20 w-20 rounded-xl bg-violet-600"
  drag
  :whileDrag="{ scale: 1.08 }"
/>
```

Ограничение по оси:

```vue
<motion.div drag="x" />
```

Ограничение области:

```vue
<motion.div
  drag="x"
  :dragConstraints="{ left: 0, right: 300 }"
  :dragElastic="0.2"
  :dragMomentum="false"
/>
```

## Touch input и pan/drag

Для корректной работы pan gestures на touch devices часто нужно CSS-правило:

```css
.draggable {
  touch-action: none;
}
```

Иначе браузер может воспринимать движение как scroll/zoom gesture.

## Мини-шпаргалка

- `whileHover` - hover state.
- `whilePress` - press/tap state.
- `whileFocus` - focus state.
- `drag` включает drag.
- `drag="x"` или `drag="y"` ограничивает ось.
- `dragConstraints` ограничивает область.
- Для touch gestures помни про `touch-action`.
