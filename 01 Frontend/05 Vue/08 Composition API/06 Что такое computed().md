# Что такое computed()?

> [!NOTE]
> `computed()` создает кэшируемое реактивное значение, которое зависит от других реактивных данных и пересчитывается только при их изменении.

## Вопрос

Что такое `computed()`?

## Базовый пример

```typescript
import { computed, ref } from "vue";

const price = ref(100);
const count = ref(2);

const total = computed(() => price.value * count.value);
```

`total` пересчитается, когда изменится `price` или `count`.

## В шаблоне

```vue
<template>
  <p>Итого: {{ total }}</p>
</template>
```

В template `.value` писать не нужно.

## Почему computed лучше метода

Computed кэширует результат. Метод выполняется при каждом вызове в рендере.

```typescript
const fullName = computed(() => `${firstName.value} ${lastName.value}`);
```

## Writable computed

```typescript
const fullName = computed({
  get: () => `${firstName.value} ${lastName.value}`,
  set: (value: string) => {
    [firstName.value, lastName.value] = value.split(" ");
  },
});
```

## Мини-шпаргалка

- `computed` нужен для производных данных.
- Кэшируется по зависимостям.
- Не предназначен для side effects.
- Для side effects используй `watch`.
