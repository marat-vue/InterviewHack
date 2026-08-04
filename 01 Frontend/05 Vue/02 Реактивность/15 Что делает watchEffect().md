# Что делает watchEffect()?

> [!NOTE] Коротко
> `watchEffect()` сразу запускает функцию и автоматически отслеживает все реактивные значения, которые были прочитаны внутри нее.

## Вопрос

Что делает `watchEffect()`?

## Базовый пример

```typescript
import { ref, watchEffect } from "vue";

const count = ref(0);

watchEffect(() => {
  console.log("count:", count.value);
});

count.value++;
```

Функция запустится сразу, а затем снова при изменении `count`.

## Отличие от watch

`watch` требует явно указать источник. `watchEffect` собирает зависимости автоматически.

```typescript
watch(search, (value) => {
  console.log(value);
});

watchEffect(() => {
  console.log(search.value);
});
```

## Очистка side effect

```typescript
watchEffect((onCleanup) => {
  const id = setInterval(() => {
    console.log(count.value);
  }, 1000);

  onCleanup(() => clearInterval(id));
});
```

Очистка нужна для таймеров, подписок и отмены устаревших действий.

## Когда использовать

`watchEffect` удобен, когда зависимостей несколько или они меняются, а тебе не нужно сравнивать новое и старое значение.

## Мини-шпаргалка

- Запускается сразу.
- Сам собирает зависимости.
- Не дает `oldValue`.
- Для точного контроля источника используй `watch`.
- Для подписок используй cleanup.
