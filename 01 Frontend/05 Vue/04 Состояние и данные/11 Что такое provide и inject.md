# Что такое provide и inject?

> [!NOTE] Коротко
> `provide` и `inject` позволяют передать значение глубоко в дерево компонентов без проброса props через каждый промежуточный компонент.

## Вопрос

Что такое `provide` и `inject`?

## Проблема prop drilling

Иногда значение нужно компоненту на третьем или четвертом уровне вложенности.

```text
App -> Layout -> Sidebar -> UserMenu
```

Передавать prop через все уровни неудобно, если промежуточные компоненты сами его не используют.

## provide

```vue
<script setup>
import { provide, ref } from "vue";

const theme = ref("dark");

provide("theme", theme);
</script>
```

Родитель или верхний компонент предоставляет значение.

## inject

```vue
<script setup>
import { inject } from "vue";
import type { Ref } from "vue";

const theme = inject<Ref<string>>("theme");
</script>
```

Дочерний компонент получает значение, даже если между ним и provider есть несколько уровней.

## Лучше использовать Symbol

```typescript
export const themeKey = Symbol("theme");
```

`Symbol` снижает риск конфликта строковых ключей.

## Когда использовать

`provide/inject` подходят для темы, локального контекста формы, зависимостей layout-а или библиотеки компонентов. Для глобального бизнес-состояния часто лучше Pinia.

## Мини-шпаргалка

- `provide` передает значение вниз по дереву.
- `inject` получает значение у потомка.
- Не нужно пробрасывать props через промежуточные компоненты.
- Для типизации и уникальности удобно использовать `Symbol`.
- Не заменяй этим весь state management.
