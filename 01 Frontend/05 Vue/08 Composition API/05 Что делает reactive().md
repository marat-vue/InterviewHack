# Что делает reactive()?

> [!NOTE]
> `reactive()` делает объект реактивным через Proxy. Vue отслеживает чтение и изменение его свойств и обновляет зависимые вычисления или компоненты.

## Вопрос

Что делает `reactive()`?

## Базовый пример

```vue
<script setup>
import { reactive } from "vue";

const form = reactive({
  email: "",
  password: "",
});
</script>

<template>
  <input v-model="form.email" />
  <input v-model="form.password" type="password" />
</template>
```

Поля `form.email` и `form.password` реактивны.

## Отличие от ref

`reactive` используют для объектов и коллекций. `ref` удобнее для примитивов или значения, которое заменяется целиком.

```typescript
const count = ref(0);
const user = reactive({ name: "Анна" });
```

## Proxy-объект

```typescript
const raw = { count: 0 };
const state = reactive(raw);

console.log(raw === state); // false
```

Работать нужно с объектом, который вернул `reactive`.

## Деструктуризация

```typescript
const state = reactive({ count: 0 });
const { count } = state; // обычное число
```

Чтобы сохранить реактивность при деструктуризации, используй `toRefs`.

## Мини-шпаргалка

- `reactive(object)` возвращает Proxy.
- В script не нужен `.value`.
- Подходит для объектов форм и сложного state.
- Неаккуратная деструктуризация теряет реактивность.
