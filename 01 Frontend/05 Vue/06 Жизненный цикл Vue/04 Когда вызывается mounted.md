# Когда вызывается mounted?

> [!NOTE] Коротко
> `mounted` вызывается после того, как компонент впервые отрендерен и вставлен в DOM. В Composition API ему соответствует `onMounted`.

## Вопрос

Когда вызывается `mounted`?

## Базовый пример Options API

```javascript
export default {
  mounted() {
    console.log("Компонент уже в DOM");
  },
};
```

На этом этапе можно обращаться к DOM-элементам компонента.

## Composition API

```vue
<script setup>
import { onMounted } from "vue";

onMounted(() => {
  console.log("DOM готов");
});
</script>
```

## Работа с template ref

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

Template refs становятся надежно доступны после монтирования.

## Что делать в mounted

В `mounted` часто подключают сторонние DOM-библиотеки, ставят фокус, читают размеры элементов, запускают подписки или делают стартовые действия, которым нужен DOM.

## Мини-шпаргалка

- `mounted` вызывается после вставки компонента в DOM.
- В Composition API используется `onMounted`.
- Template refs доступны именно здесь.
- Для очистки созданных side effects используй `unmounted/onUnmounted`.
