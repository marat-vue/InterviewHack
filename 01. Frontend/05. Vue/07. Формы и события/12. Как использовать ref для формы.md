# Как использовать ref для формы?

> [!NOTE]
> `ref` удобно использовать для отдельных полей формы, простых значений и template refs на DOM-элементы формы.

## Вопрос

Как использовать `ref` для формы?

## Отдельные поля

```vue
<script setup>
import { ref } from "vue";

const email = ref("");
const password = ref("");
const isSubmitting = ref(false);
</script>

<template>
  <input v-model="email" />
  <input v-model="password" type="password" />
  <button :disabled="isSubmitting">Войти</button>
</template>
```

Каждое поле хранится в отдельном `ref`.

## Отправка формы

```typescript
async function submit() {
  isSubmitting.value = true;

  try {
    await login({
      email: email.value,
      password: password.value,
    });
  } finally {
    isSubmitting.value = false;
  }
}
```

В script значения refs читаются через `.value`.

## Template ref на форму

```vue
<script setup>
import { ref } from "vue";

const formRef = ref<HTMLFormElement | null>(null);

function resetNativeForm() {
  formRef.value?.reset();
}
</script>

<template>
  <form ref="formRef" @submit.prevent="submit">
    ...
  </form>
</template>
```

## Когда ref удобнее reactive

`ref` хорош, если полей мало, они независимы или значение часто заменяется целиком.

## Мини-шпаргалка

- Для отдельных полей: `const email = ref("")`.
- В template `.value` не нужен.
- В script нужен `.value`.
- DOM form ref доступен после mount.
- Для большой формы часто удобнее `reactive`.
