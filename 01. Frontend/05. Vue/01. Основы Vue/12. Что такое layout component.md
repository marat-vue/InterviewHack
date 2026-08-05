# Что такое layout component?

> [!NOTE]
> Layout component - компонент, который задает общую структуру страницы: шапку, боковую панель, основную область, футер и места для контента.

## Вопрос

Что такое `layout component`?

## Главная идея

Layout отделяет каркас страницы от конкретного содержимого. Страницы меняются, а общая структура остается одной.

```vue
<!-- AppLayout.vue -->
<template>
  <div class="layout">
    <AppHeader />
    <aside><slot name="sidebar" /></aside>
    <main><slot /></main>
  </div>
</template>
```

```vue
<!-- ProfilePage.vue -->
<template>
  <AppLayout>
    <template #sidebar>
      <ProfileMenu />
    </template>

    <UserProfile />
  </AppLayout>
</template>
```

## Что обычно содержит layout

- Общую навигацию.
- Область для контента страницы.
- Сайдбар или панель действий.
- Общие провайдеры, wrappers, иногда обработку loading/error.

## Почему это удобно

Layout снижает дублирование: не нужно копировать header, sidebar и общий каркас в каждую страницу.

## Layout и роутинг

В SPA layout часто используют вместе с Vue Router: разные группы маршрутов могут иметь разные layout-компоненты.

## Мини-шпаргалка

- Layout задает каркас страницы.
- Контент обычно передается через slots.
- Помогает не дублировать общие части UI.
- Может отличаться для публичной, личной и админской зон.
