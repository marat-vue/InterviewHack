# Какие преимущества дает Composition API?

> [!NOTE]
> Composition API улучшает организацию сложной логики, упрощает переиспользование через composables и хорошо сочетается с TypeScript.

## Вопрос

Какие преимущества дает Composition API?

## Логика группируется по смыслу

В Options API одна фича может быть разбросана по `data`, `computed`, `methods`, `watch`. В Composition API ее можно держать рядом.

```typescript
const search = ref("");
const results = ref<User[]>([]);

watch(search, async (value) => {
  results.value = await fetchUsers(value);
});
```

## Переиспользование через composables

```typescript
export function useSearch() {
  const query = ref("");
  const results = ref<string[]>([]);

  return { query, results };
}
```

Composable можно подключать в разных компонентах без mixins.

## TypeScript

Composition API обычно дает более прямую и понятную типизацию.

```typescript
const user = ref<User | null>(null);
const items = reactive<CartItem[]>([]);
```

## Удобство для больших компонентов

Можно выделять независимые блоки логики: форму, загрузку данных, фильтры, подписки, работу с DOM.

## Мини-шпаргалка

- Логика группируется по фичам.
- Composables заменяют многие сценарии mixins.
- TypeScript работает естественнее.
- Большие компоненты проще делить на части.
