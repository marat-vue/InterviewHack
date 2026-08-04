# Для чего используется v-bind?

> [!NOTE] Коротко
> `v-bind` связывает HTML-атрибут или prop компонента с JavaScript-выражением. Сокращенная запись - `:`.

## Вопрос

Для чего используется `v-bind`?

## Атрибуты HTML

```vue
<script setup>
const url = "/profile";
const isDisabled = true;
</script>

<template>
  <a v-bind:href="url">Профиль</a>
  <button v-bind:disabled="isDisabled">Сохранить</button>
</template>
```

Если `url` или `isDisabled` изменятся, Vue обновит атрибут.

## Сокращенная запись

```vue
<a :href="url">Профиль</a>
<button :disabled="isDisabled">Сохранить</button>
```

На практике чаще используют сокращение `:`.

## Props компонентов

```vue
<UserCard :user="currentUser" :is-active="true" />
```

`v-bind` передает динамические props в дочерний компонент.

## Объект атрибутов

```vue
<script setup>
const attrs = {
  id: "save-button",
  disabled: false,
};
</script>

<template>
  <button v-bind="attrs">Сохранить</button>
</template>
```

Так можно передать сразу набор атрибутов.

## Мини-шпаргалка

- `v-bind:attr="value"` связывает атрибут с выражением.
- `:attr="value"` - короткая запись.
- Для props компонентов тоже используют `:prop`.
- `v-bind="object"` передает несколько атрибутов сразу.
