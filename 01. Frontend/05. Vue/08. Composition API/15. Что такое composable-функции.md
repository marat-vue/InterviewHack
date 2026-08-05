# Что такое composable-функции?

> [!NOTE]
> Composable - функция, которая использует Composition API и возвращает переиспользуемую реактивную логику: state, computed, методы, watchers или lifecycle hooks.

## Вопрос

Что такое composable-функции?

## Базовый пример

```typescript
import { computed, ref } from "vue";

export function useCounter(initialValue = 0) {
  const count = ref(initialValue);
  const doubled = computed(() => count.value * 2);
  const increment = () => count.value++;

  return { count, doubled, increment };
}
```

В компоненте:

```vue
<script setup>
const { count, doubled, increment } = useCounter();
</script>
```

## Зачем нужны composables

Они выносят повторяемую логику из компонентов: загрузку данных, работу с localStorage, форму, фильтры, подписки, состояние модалки.

## Правило именования

Composable обычно называют с префиксом `use`.

```typescript
useFetch();
useWindowSize();
useUserForm();
```

## Важный нюанс

Если composable создает state внутри функции, каждый вызов получает отдельный state. Если state объявлен снаружи функции, он становится общим.

```typescript
const shared = ref(0);

export function useSharedCounter() {
  return { shared };
}
```

## Мини-шпаргалка

- Composable - функция с Composition API логикой.
- Возвращает refs, computed и методы.
- Обычно называется `useSomething`.
- Помогает заменить mixins более явной композицией.
- Следи, локальный state внутри функции или общий снаружи.
