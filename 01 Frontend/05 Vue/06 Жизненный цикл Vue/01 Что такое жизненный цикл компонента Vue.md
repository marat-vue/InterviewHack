# Что такое жизненный цикл компонента Vue?

> [!NOTE] Коротко
> Жизненный цикл компонента Vue - последовательность этапов от создания компонента до его удаления: setup, mount, update и unmount.

## Вопрос

Что такое жизненный цикл компонента Vue?

## Основная идея

Компонент не просто "существует". Он создается, подготавливает реактивность, рендерится, попадает в DOM, обновляется при изменениях и затем удаляется.

```text
create -> mount -> update -> unmount
```

На разных этапах Vue дает lifecycle hooks.

## Пример Composition API

```vue
<script setup>
import { onMounted, onUnmounted } from "vue";

onMounted(() => {
  console.log("DOM готов");
});

onUnmounted(() => {
  console.log("Компонент удален");
});
</script>
```

## Пример Options API

```javascript
export default {
  mounted() {
    console.log("DOM готов");
  },
  unmounted() {
    console.log("Компонент удален");
  },
};
```

## Зачем нужны хуки

Хуки позволяют выполнить код в правильный момент: сделать запрос, подключить стороннюю библиотеку, прочитать DOM, очистить таймер или подписку.

## Мини-шпаргалка

- Lifecycle описывает этапы жизни компонента.
- `mounted` - компонент в DOM.
- `updated` - DOM обновился.
- `unmounted` - компонент удален.
- Side effects нужно очищать при unmount.
