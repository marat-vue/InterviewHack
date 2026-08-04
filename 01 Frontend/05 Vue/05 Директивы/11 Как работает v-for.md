# Как работает v-for?

> [!NOTE] Коротко
> `v-for` рендерит список элементов по массиву, объекту или диапазону. Для стабильного обновления списка почти всегда нужен уникальный `:key`.

## Вопрос

Как работает `v-for`?

## Список по массиву

```vue
<script setup>
const todos = [
  { id: 1, title: "Выучить Vue" },
  { id: 2, title: "Сделать проект" },
];
</script>

<template>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.title }}
    </li>
  </ul>
</template>
```

Vue создаст `li` для каждого элемента массива.

## Индекс элемента

```vue
<li v-for="(todo, index) in todos" :key="todo.id">
  {{ index + 1 }}. {{ todo.title }}
</li>
```

Индекс полезен для отображения номера, но обычно плох как `key`, если список может изменяться.

## Перебор объекта

```vue
<li v-for="(value, key) in user" :key="key">
  {{ key }}: {{ value }}
</li>
```

## v-for с компонентом

```vue
<UserCard
  v-for="user in users"
  :key="user.id"
  :user="user"
/>
```

`key` помогает Vue сопоставлять старые и новые элементы при обновлении.

## Мини-шпаргалка

- `v-for="item in items"` рендерит список.
- Можно получить индекс: `(item, index) in items`.
- Для объектов: `(value, key) in object`.
- Всегда добавляй стабильный `:key`.
- Не используй индекс как key для изменяемых списков.
