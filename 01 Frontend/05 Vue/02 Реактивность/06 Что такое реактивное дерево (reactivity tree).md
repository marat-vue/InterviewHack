# Что такое реактивное дерево (reactivity tree)?

> [!NOTE]
> Реактивное дерево - мысленная модель зависимостей между реактивными данными, computed, watchers и компонентами. Когда один узел меняется, Vue обновляет зависящие от него части.

## Вопрос

Что такое реактивное дерево во Vue?

## Простая модель

```text
count -> doubled -> template
```

Если меняется `count`, Vue понимает, что нужно пересчитать `doubled` и обновить шаблон, где он используется.

## Пример

```vue
<script setup>
import { computed, ref, watch } from "vue";

const count = ref(1);
const doubled = computed(() => count.value * 2);

watch(doubled, (value) => {
  console.log("Новое значение:", value);
});
</script>

<template>
  <p>{{ doubled }}</p>
  <button @click="count++">+</button>
</template>
```

Зависимости можно представить так:

```text
count
  -> doubled
    -> watch(doubled)
    -> component render
```

## Почему это полезно понимать

Реактивное дерево помогает объяснить, почему изменение одного значения вызывает перерендер, пересчет computed или запуск watcher.

## Где бывают ошибки

Если вынести значение из реактивного объекта без сохранения связи, зависимость может потеряться.

```typescript
const state = reactive({ count: 0 });
const count = state.count; // обычное число, не ref
```

Для сохранения связи используют `toRef` или `toRefs`.

## Мини-шпаргалка

- Реактивное дерево показывает зависимости.
- Узлы: `ref`, `reactive`, `computed`, `watch`, render.
- Изменение источника уведомляет зависимые узлы.
- Потеря связи часто возникает при неаккуратной деструктуризации.
