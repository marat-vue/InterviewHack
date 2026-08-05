# Что такое props?

> [!NOTE]
> Props - входные параметры компонента. Родитель передает данные вниз, а дочерний компонент читает их как readonly-значения.

## Вопрос

Что такое props во Vue?

## Базовый пример

```vue
<!-- Parent.vue -->
<template>
  <UserCard name="Анна" :age="28" />
</template>
```

```vue
<!-- UserCard.vue -->
<script setup>
defineProps<{
  name: string;
  age: number;
}>();
</script>

<template>
  <h2>{{ name }}</h2>
  <p>{{ age }}</p>
</template>
```

## Зачем нужны props

Props делают компонент настраиваемым и переиспользуемым. Один `UserCard` может показать разных пользователей, получая разные входные данные.

## Props readonly

Дочерний компонент не должен менять props напрямую.

```vue
<script setup>
const props = defineProps<{ count: number }>();

// props.count++; // ошибка
</script>
```

Чтобы изменить состояние родителя, ребенок отправляет событие через `emit`.

## Значения по умолчанию

```vue
<script setup>
const props = withDefaults(defineProps<{ size?: "sm" | "md" }>(), {
  size: "md",
});
</script>
```

## Мини-шпаргалка

- Props передаются от родителя к ребенку.
- В шаблоне динамические props пишут через `:prop`.
- Props readonly внутри дочернего компонента.
- Для обратной связи используй `emit`.
