# Какие хуки жизненного цикла доступны в Composition API?

> [!NOTE] Коротко
> В Composition API хуки жизненного цикла доступны как функции `onMounted`, `onUpdated`, `onUnmounted` и другие. Их вызывают синхронно внутри `setup` или `<script setup>`.

## Вопрос

Какие хуки жизненного цикла доступны в Composition API?

## Основные хуки

```typescript
import {
  onBeforeMount,
  onMounted,
  onBeforeUpdate,
  onUpdated,
  onBeforeUnmount,
  onUnmounted,
} from "vue";
```

Эти хуки соответствуют этапам mount, update и unmount.

## Пример

```vue
<script setup>
import { onMounted, onUnmounted } from "vue";

onMounted(() => {
  window.addEventListener("resize", onResize);
});

onUnmounted(() => {
  window.removeEventListener("resize", onResize);
});

function onResize() {
  console.log(window.innerWidth);
}
</script>
```

## Дополнительные хуки

```typescript
import {
  onActivated,
  onDeactivated,
  onErrorCaptured,
  onRenderTracked,
  onRenderTriggered,
} from "vue";
```

`onActivated` и `onDeactivated` связаны с `keep-alive`. Debug-хуки помогают понять, какие зависимости вызывают рендер.

## Важное правило

Lifecycle hooks нужно регистрировать синхронно во время `setup`.

```typescript
onMounted(() => {
  console.log("ok");
});
```

Не стоит вызывать `onMounted` внутри `setTimeout`, `then` или обработчика клика.

## Мини-шпаргалка

- Composition API хуки начинаются с `on`.
- `onMounted` - DOM готов.
- `onUpdated` - DOM обновился.
- `onUnmounted` - компонент удален.
- Для `keep-alive`: `onActivated`, `onDeactivated`.
