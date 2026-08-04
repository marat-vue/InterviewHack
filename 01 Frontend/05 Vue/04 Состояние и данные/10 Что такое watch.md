# Что такое watch?

> [!NOTE] Коротко
> `watch` отслеживает изменение реактивного источника и запускает callback. Он нужен для side effects: запросов, логирования, синхронизации с внешним миром.

## Вопрос

Что такое `watch` во Vue?

## Базовый пример

```vue
<script setup>
import { ref, watch } from "vue";

const query = ref("");

watch(query, (newQuery, oldQuery) => {
  console.log("Было:", oldQuery);
  console.log("Стало:", newQuery);
});
</script>
```

`watch` не вычисляет значение для шаблона. Он реагирует на изменение.

## Запрос при изменении

```typescript
watch(query, async (value) => {
  if (value.length < 3) return;

  await fetch(`/api/search?q=${encodeURIComponent(value)}`);
});
```

## Несколько источников

```typescript
watch([page, query], ([newPage, newQuery]) => {
  console.log(newPage, newQuery);
});
```

## watch против computed

`computed` нужен для производного значения. `watch` нужен для побочного эффекта.

```typescript
const total = computed(() => price.value * count.value);
```

Если результата можно избежать как отдельного side effect, выбирай `computed`.

## Мини-шпаргалка

- `watch` следит за источником.
- Callback получает новое и старое значение.
- Подходит для side effects.
- Для производных значений используй `computed`.
- Для автоматического сбора зависимостей есть `watchEffect`.
