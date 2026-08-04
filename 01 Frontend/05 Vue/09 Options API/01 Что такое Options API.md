# Что такое Options API?

> [!NOTE] Коротко
> Options API - классический способ писать Vue-компоненты через объект с опциями: `data`, `methods`, `computed`, `watch`, `props`, `emits` и lifecycle hooks.

## Вопрос

Что такое Options API?

## Базовый пример

```vue
<script>
export default {
  data() {
    return {
      count: 0,
    };
  },
  computed: {
    doubled() {
      return this.count * 2;
    },
  },
  methods: {
    increment() {
      this.count++;
    },
  },
};
</script>

<template>
  <button @click="increment">{{ doubled }}</button>
</template>
```

Логика группируется по типу опции.

## Основные опции

- `data` - локальное состояние.
- `methods` - методы и обработчики.
- `computed` - вычисляемые значения.
- `watch` - реакции на изменения.
- `props` - входные данные.
- `emits` - события компонента.
- `mounted`, `updated`, `unmounted` - lifecycle hooks.

## Когда удобен

Options API прост для обучения, хорошо читается в небольших компонентах и часто встречается в проектах Vue 2.

## Ограничение

В больших компонентах связанная логика может оказаться разбросанной по разным опциям.

## Мини-шпаргалка

- Options API = компонент как объект опций.
- `this` дает доступ к state, methods и computed.
- Хорош для простых и legacy-компонентов.
- В Vue 3 можно использовать вместе с Composition API.
