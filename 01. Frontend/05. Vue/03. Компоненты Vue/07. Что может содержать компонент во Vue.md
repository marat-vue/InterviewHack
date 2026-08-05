# Что может содержать компонент во Vue?

> [!NOTE]
> Компонент Vue может содержать состояние, props, computed, methods, watchers, lifecycle hooks, дочерние компоненты, slots, emits и стили.

## Вопрос

Что может содержать компонент во Vue?

## В Single File Component

```vue
<script setup>
import { computed, ref } from "vue";

const count = ref(0);
const doubled = computed(() => count.value * 2);
</script>

<template>
  <button @click="count++">{{ doubled }}</button>
</template>

<style scoped>
button {
  color: royalblue;
}
</style>
```

SFC объединяет логику, шаблон и стили компонента.

## Основные части

- State: локальные данные компонента.
- Props: входные данные от родителя.
- Emits: события наружу.
- Computed: производные значения.
- Watchers: side effects при изменениях.
- Slots: переданный родителем шаблон.
- Lifecycle hooks: код на этапах жизни компонента.

## Компонент может быть простым

```vue
<template>
  <hr />
</template>
```

Не каждый компонент обязан иметь состояние или script.

## Компонент может быть контейнером

Контейнерные компоненты часто загружают данные и передают их вниз в презентационные компоненты.

## Мини-шпаргалка

- Минимальный компонент может содержать только template.
- SFC часто содержит `script`, `template`, `style`.
- Props и emits описывают внешний контракт.
- Slots дают гибкость для вложенного шаблона.
