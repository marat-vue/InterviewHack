# Что такое watch()?

> [!NOTE]
> `watch()` следит за выбранным реактивным источником и запускает callback при изменении. Это инструмент для side effects.

## Вопрос

Что такое `watch()`?

## Базовый пример

```typescript
import { ref, watch } from "vue";

const query = ref("");

watch(query, (newValue, oldValue) => {
  console.log(newValue, oldValue);
});
```

`watch` получает новое и старое значение.

## Источник как getter

```typescript
watch(
  () => user.value?.id,
  (id) => {
    if (id) loadUserDetails(id);
  }
);
```

Getter удобен, когда нужно следить не за всем объектом, а за конкретным выражением.

## Несколько источников

```typescript
watch([page, query], ([newPage, newQuery]) => {
  loadResults(newPage, newQuery);
});
```

## Очистка

```typescript
watch(query, async (value, _oldValue, onCleanup) => {
  const controller = new AbortController();
  onCleanup(() => controller.abort());

  await fetch(`/api?q=${value}`, { signal: controller.signal });
});
```

Cleanup помогает отменять устаревшие side effects.

## Мини-шпаргалка

- `watch(source, callback)` следит за источником.
- Подходит для запросов, синхронизации и подписок.
- Для нескольких источников передай массив.
- Для автосбора зависимостей есть `watchEffect`.
