# Как использовать useRoute и useRouter?

> [!NOTE]
> `useRoute` дает текущий route: params, query, meta, path. `useRouter` дает router instance: `push`, `replace`, `back`, `beforeEach` и другие методы навигации.

## useRoute

```typescript
import { useRoute } from "vue-router";

const route = useRoute();

console.log(route.params.id);
console.log(route.query.page);
console.log(route.meta.requiresAuth);
```

`route` reactive. Если URL изменится, значения обновятся.

## useRouter

```typescript
import { useRouter } from "vue-router";

const router = useRouter();

function goToProfile(id: number) {
  router.push({
    name: "user-details",
    params: { id },
  });
}
```

## push vs replace

```typescript
router.push("/settings");
router.replace("/login");
```

`push` добавляет запись в history. `replace` заменяет текущую запись. После `replace` кнопка Back не вернет на старый route.

`replace` часто используют после login/logout redirect.

## back и forward

```typescript
router.back();
router.forward();
```

Это обертки над browser history.

## Query update без потери старых query

```typescript
router.push({
  query: {
    ...route.query,
    page: 2,
  },
});
```

Так можно обновить один параметр списка и сохранить остальные фильтры.

## Мини-шпаргалка

- `useRoute` читает текущий route.
- `useRouter` выполняет навигацию.
- `router.push` добавляет history entry.
- `router.replace` заменяет history entry.
- Route object reactive.
- Для query updates сохраняй старые query, если они нужны.
