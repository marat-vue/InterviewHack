# Что такое ref()?

> [!NOTE] Коротко
> `ref()` создает реактивную обертку для значения. В JavaScript значение доступно через `.value`, а в шаблоне Vue разворачивает ref автоматически.

## Вопрос

Что такое `ref()`?

## Базовый пример

```vue
<script setup>
import { ref } from "vue";

const count = ref(0);

function increment() {
  count.value++;
}
</script>

<template>
  <button @click="increment">{{ count }}</button>
</template>
```

В `<script setup>` нужно писать `count.value`, в template можно писать `count`.

## Типизация

```typescript
const name = ref("Анна");
const user = ref<User | null>(null);
```

TypeScript выводит тип из начального значения, но для `null` часто нужен явный generic.

## Ref для DOM

```vue
<script setup>
import { onMounted, ref } from "vue";

const inputRef = ref<HTMLInputElement | null>(null);

onMounted(() => {
  inputRef.value?.focus();
});
</script>

<template>
  <input ref="inputRef" />
</template>
```

## Когда выбирать ref

`ref` удобен для примитивов, nullable-значений, DOM-ссылок и случаев, где значение заменяется целиком.

## Мини-шпаргалка

- `ref(value)` делает значение реактивным.
- В script: `.value`.
- В template: авторазворачивание.
- Для `null` часто пишут `ref<Type | null>(null)`.
