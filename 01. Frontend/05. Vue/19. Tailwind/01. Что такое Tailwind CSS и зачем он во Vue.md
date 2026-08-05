# Что такое Tailwind CSS и зачем он во Vue?

> [!NOTE]
> Tailwind CSS - utility-first CSS framework. Вместо готовых компонентов он дает маленькие CSS-классы вроде `flex`, `gap-4`, `text-sm`, `bg-blue-600`, из которых быстро собирают интерфейс прямо в шаблоне Vue.

## Главная идея

Обычный CSS:

```vue
<template>
  <button class="primary-button">Сохранить</button>
</template>

<style scoped>
.primary-button {
  padding: 8px 16px;
  border-radius: 8px;
  background: #2563eb;
  color: white;
}
</style>
```

Tailwind:

```vue
<template>
  <button class="rounded-lg bg-blue-600 px-4 py-2 text-white">
    Сохранить
  </button>
</template>
```

## Что Tailwind дает Vue-разработчику?

- быстрый layout без постоянного переключения в CSS;
- единые design tokens;
- responsive modifiers;
- hover/focus/dark variants;
- меньше случайных имен классов;
- удобную работу с компонентами.

## Tailwind - это не UI kit

Tailwind не дает готовых Vue-компонентов вроде `Button` или `Dialog`. Он дает CSS utilities.

Если нужны готовые компоненты, смотри Vuetify, PrimeVue, Headless UI или собственный design system.

## Когда Tailwind особенно хорош?

- custom дизайн;
- landing pages;
- design system;
- быстрые MVP;
- команды, которым нравится utility-first подход;
- компоненты с точным контролем внешнего вида.

## Мини-шпаргалка

- Tailwind - utility-first CSS framework.
- Классы пишутся прямо в template.
- Tailwind не является Vue component library.
- Хорош для custom UI.
- Требует дисциплины, иначе class lists становятся шумными.
