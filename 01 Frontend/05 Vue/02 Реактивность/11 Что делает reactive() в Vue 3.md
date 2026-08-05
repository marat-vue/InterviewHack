# Что делает reactive() в Vue 3?

> [!NOTE]
> `reactive()` делает объект реактивным через Proxy. Vue отслеживает чтение и изменение его свойств и обновляет зависимый код.

## Вопрос

Что делает `reactive()` в Vue 3?

## Базовый пример

```typescript
import { reactive } from "vue";

const state = reactive({
  count: 0,
  user: {
    name: "Анна",
  },
});

state.count++;
state.user.name = "Мария";
```

`state` - proxy-объект. Работать нужно именно с ним.

## В шаблоне

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

## Чем отличается от ref

`reactive` удобен для объектов с несколькими связанными полями. `ref` чаще используют для одного значения или когда нужно сохранить реактивность при замене целиком.

```typescript
const count = ref(0);
const user = reactive({ name: "Анна" });
```

## Важный нюанс с деструктуризацией

```typescript
const state = reactive({ count: 0 });
const { count } = state;
```

`count` станет обычным числом. Чтобы сохранить реактивность, используй `toRefs`.

## Мини-шпаргалка

- `reactive(object)` возвращает Proxy.
- Подходит для объектов и коллекций.
- Не требует `.value`.
- Деструктуризация может потерять реактивность.
- Для примитивов используй `ref`.
