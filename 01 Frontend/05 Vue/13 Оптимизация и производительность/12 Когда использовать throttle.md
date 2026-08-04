# Когда использовать throttle?

> [!NOTE]
> **Throttle** ограничивает частоту вызова функции: она выполняется не чаще одного раза за заданный интервал, даже если событие происходит очень часто.

## Главное

Throttle нужен, когда поток событий идет постоянно, а приложение должно регулярно, но не слишком часто, реагировать на него.

```text
events:   x x x x x x x x x x x
throttle: x-----x-----x-----x---
```

Например, пользователь скроллит страницу десятки раз в секунду, а обработчик нужно запускать раз в `200ms`.

## Где использовать

- `scroll`;
- `resize`;
- drag-and-drop;
- перемещение мыши;
- отслеживание позиции;
- периодическое сохранение прогресса;
- обновление графиков или координат.

## Пример

```js
function throttle(callback, delay) {
  let lastCall = 0;

  return (...args) => {
    const now = Date.now();

    if (now - lastCall >= delay) {
      lastCall = now;
      callback(...args);
    }
  };
}
```

```vue
<script setup>
import { onBeforeUnmount, onMounted, ref } from "vue";

const scrollY = ref(0);

const handleScroll = throttle(() => {
  scrollY.value = window.scrollY;
}, 200);

onMounted(() => {
  window.addEventListener("scroll", handleScroll);
});

onBeforeUnmount(() => {
  window.removeEventListener("scroll", handleScroll);
});
</script>
```

## Throttle или debounce

Throttle выполняется регулярно во время события. Debounce ждет, пока поток событий закончится.

```text
scroll position indicator -> throttle
search input request      -> debounce
```

## Мини-шпаргалка

- Throttle ограничивает частоту выполнения.
- Подходит для событий, которые идут непрерывно.
- Функция может вызываться во время потока событий.
- Частые сценарии: scroll, resize, drag.
- Для ожидания конца ввода лучше debounce.
