# Что такое вычисляемые свойства (computed)?

> [!NOTE]
> `computed` - реактивное производное значение, которое вычисляется из других реактивных данных и кэшируется, пока зависимости не изменились.

## Вопрос

Что такое вычисляемые свойства (`computed`) во Vue?

## Базовый пример

```vue
<script setup>
import { computed, ref } from "vue";

const firstName = ref("Анна");
const lastName = ref("Петрова");

const fullName = computed(() => `${firstName.value} ${lastName.value}`);
</script>

<template>
  <p>{{ fullName }}</p>
</template>
```

`fullName` пересчитается только при изменении `firstName` или `lastName`.

## Почему не хранить это в state

Если значение можно вывести из других данных, его лучше не дублировать в state.

```typescript
const price = ref(100);
const count = ref(2);
const total = computed(() => price.value * count.value);
```

Так меньше риска, что `total` станет неактуальным.

## Writable computed

Иногда computed можно сделать с getter и setter.

```typescript
const fullName = computed({
  get: () => `${firstName.value} ${lastName.value}`,
  set: (value: string) => {
    [firstName.value, lastName.value] = value.split(" ");
  },
});
```

## Мини-шпаргалка

- `computed` описывает производное состояние.
- Кэшируется до изменения зависимостей.
- Лучше, чем метод, если результат зависит от state и используется в template.
- Не используй `computed` для side effects, для этого есть `watch`.
