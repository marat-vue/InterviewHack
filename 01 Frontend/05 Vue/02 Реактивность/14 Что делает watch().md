# Что делает watch()?

> [!NOTE] Коротко
> `watch()` следит за конкретным реактивным источником и запускает callback, когда значение изменилось. Он подходит для side effects: запросов, синхронизации, логирования, работы с внешними API.

## Вопрос

Что делает `watch()`?

## Базовый пример

```typescript
import { ref, watch } from "vue";

const search = ref("");

watch(search, (newValue, oldValue) => {
  console.log("Было:", oldValue);
  console.log("Стало:", newValue);
});
```

`watch` получает новое и старое значение.

## Watch для computed/getter

```typescript
const firstName = ref("Анна");
const lastName = ref("Петрова");

watch(
  () => `${firstName.value} ${lastName.value}`,
  (fullName) => {
    console.log(fullName);
  }
);
```

## Несколько источников

```typescript
watch([firstName, lastName], ([newFirst, newLast]) => {
  console.log(newFirst, newLast);
});
```

## Опции

```typescript
watch(
  search,
  (value) => {
    fetch(`/api?q=${value}`);
  },
  { immediate: true }
);
```

`immediate` запускает watcher сразу, а `deep` нужен для глубокого наблюдения за объектом.

## Мини-шпаргалка

- `watch(source, callback)` следит за источником.
- Callback получает `newValue` и `oldValue`.
- Подходит для side effects.
- Для автоматического сбора зависимостей есть `watchEffect`.
