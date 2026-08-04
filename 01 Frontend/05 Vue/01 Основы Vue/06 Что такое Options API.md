# Что такое Options API?

> [!NOTE] Коротко
> Options API - стиль написания Vue-компонентов, где логика раскладывается по опциям: `data`, `methods`, `computed`, `watch`, lifecycle hooks.

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

## Как организуется логика

В Options API код группируется по типу опции: все методы в `methods`, все вычисляемые значения в `computed`, watchers в `watch`.

## Когда удобен

Options API хорошо подходит для простых компонентов, обучения Vue и проектов, где команда привыкла к классическому стилю Vue 2.

## Ограничение

В больших компонентах связанная логика может оказаться разбросанной по разным секциям: состояние в `data`, обработчики в `methods`, сайд-эффекты в `watch`.

## Мини-шпаргалка

- Options API группирует код по опциям.
- `data()` возвращает состояние.
- `methods` содержит методы.
- `computed` хранит вычисляемые значения.
- В Vue 3 можно использовать и Options API, и Composition API.
