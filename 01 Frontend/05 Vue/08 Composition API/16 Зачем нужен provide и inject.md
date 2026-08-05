# Зачем нужен provide и inject?

> [!NOTE]
> `provide` и `inject` нужны, чтобы передавать значение глубоко вниз по дереву компонентов без prop drilling через промежуточные уровни.

## Вопрос

Зачем нужен `provide` и `inject`?

## Базовый пример

```vue
<!-- Parent.vue -->
<script setup lang="ts">
import { provide, ref } from "vue";

const theme = ref("dark");
provide("theme", theme);
</script>
```

```vue
<!-- DeepChild.vue -->
<script setup lang="ts">
import { inject } from "vue";
import type { Ref } from "vue";

const theme = inject<Ref<string>>("theme");
</script>
```

Промежуточные компоненты не обязаны принимать и передавать prop.

## С Symbol-ключом

```typescript
import type { InjectionKey, Ref } from "vue";

export const themeKey: InjectionKey<Ref<string>> = Symbol("theme");
```

```typescript
provide(themeKey, theme);
const theme = inject(themeKey);
```

Так безопаснее типизировать и труднее случайно конфликтовать с другим ключом.

## Когда использовать

Подходит для темы, контекста формы, настроек таблицы, зависимостей UI-библиотеки, локального контекста layout-а.

## Когда не использовать

Для глобального бизнес-состояния вроде пользователя или корзины часто лучше Pinia: там понятнее devtools, actions и единый store.

## Мини-шпаргалка

- `provide` отдает значение потомкам.
- `inject` получает значение ниже по дереву.
- Помогает избежать prop drilling.
- Для типизации лучше `InjectionKey`.
- Не заменяет полноценный state manager во всех случаях.
