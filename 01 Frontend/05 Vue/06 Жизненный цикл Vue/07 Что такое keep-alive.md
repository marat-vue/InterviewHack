# Что такое keep-alive?

> [!NOTE] Коротко
> `<KeepAlive>` кэширует динамические компоненты: при переключении компонент не уничтожается, а деактивируется и сохраняет свое состояние.

## Вопрос

Что такое `keep-alive` во Vue?

## Базовый пример

```vue
<template>
  <KeepAlive>
    <component :is="activeComponent" />
  </KeepAlive>
</template>
```

Когда `activeComponent` меняется, старый компонент сохраняется в кэше, а не размонтируется полностью.

## Зачем это нужно

`KeepAlive` полезен для вкладок, wizard-форм, страниц с фильтрами и компонентов, где важно сохранить локальное состояние.

```vue
<KeepAlive>
  <UserFilters v-if="showFilters" />
</KeepAlive>
```

## Lifecycle hooks

Для кэшируемых компонентов есть специальные хуки.

```vue
<script setup>
import { onActivated, onDeactivated } from "vue";

onActivated(() => {
  console.log("Компонент снова активен");
});

onDeactivated(() => {
  console.log("Компонент ушел в кэш");
});
</script>
```

## Include и exclude

```vue
<KeepAlive include="UserPage,SettingsPage" :max="10">
  <component :is="activeComponent" />
</KeepAlive>
```

Можно ограничить, какие компоненты кэшировать и сколько экземпляров хранить.

## Мини-шпаргалка

- `<KeepAlive>` кэширует компоненты.
- Состояние компонента сохраняется между переключениями.
- Вместо mount/unmount используются activated/deactivated.
- Полезен для вкладок и динамических компонентов.
