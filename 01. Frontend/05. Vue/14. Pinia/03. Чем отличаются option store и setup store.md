# Чем отличаются option store и setup store?

> [!NOTE]
> Pinia поддерживает два синтаксиса: option store похож на Options API со `state/getters/actions`, а setup store похож на Composition API с `ref`, `computed` и functions. Оба варианта официальные.

## Option store

```typescript
export const useCounterStore = defineStore("counter", {
  state: () => ({
    count: 0,
  }),
  getters: {
    doubled: (state) => state.count * 2,
  },
  actions: {
    increment() {
      this.count++;
    },
  },
});
```

Option store проще для старта: структура явно разделена на `state`, `getters`, `actions`.

## Setup store

```typescript
export const useCounterStore = defineStore("counter", () => {
  const count = ref(0);
  const doubled = computed(() => count.value * 2);

  function increment() {
    count.value++;
  }

  return { count, doubled, increment };
});
```

В setup store:

- `ref` становится state;
- `computed` становится getter;
- function становится action.

## Что выбрать?

| Ситуация | Лучше |
|---|---|
| команда только начинает с Pinia | option store |
| нужен максимально простой CRUD store | option store |
| нужны watchers внутри store | setup store |
| нужно использовать composables внутри store | setup store |
| проект активно использует Composition API | setup store часто удобнее |

## Важное правило setup store

Нужно вернуть все state-свойства, которые должны принадлежать store:

```typescript
return { count, doubled, increment };
```

Если не вернуть state, Pinia не сможет корректно работать с devtools, SSR и plugins.

## Мини-шпаргалка

- Option store = `state/getters/actions`.
- Setup store = `ref/computed/functions`.
- Оба варианта официальные.
- Для простоты часто начинают с option store.
- Для composables/watchers удобен setup store.
- В setup store возвращай все state-свойства.
