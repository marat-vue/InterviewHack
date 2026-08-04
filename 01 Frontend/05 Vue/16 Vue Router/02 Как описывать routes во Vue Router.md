# Как описывать routes во Vue Router?

> [!NOTE]
> Route record описывает URL, имя маршрута, компонент, children, redirect, alias, meta и props. Хорошая структура routes делает приложение читаемым и упрощает guards, breadcrumbs и layout logic.

## Базовый route

```typescript
{
  path: "/users",
  name: "users",
  component: () => import("@/pages/UsersPage.vue"),
}
```

## Dynamic segment

```typescript
{
  path: "/users/:id",
  name: "user-details",
  component: () => import("@/pages/UserDetailsPage.vue"),
}
```

`id` будет доступен как `route.params.id`.

## Props mode

```typescript
{
  path: "/users/:id",
  name: "user-details",
  component: () => import("@/pages/UserDetailsPage.vue"),
  props: true,
}
```

Тогда компонент может принимать `id` как prop:

```vue
<script setup lang="ts">
defineProps<{
  id: string;
}>();
</script>
```

Это уменьшает связность компонента с router.

## Redirect

```typescript
{
  path: "/home",
  redirect: "/",
}
```

## Alias

```typescript
{
  path: "/users",
  alias: "/people",
  component: UsersPage,
}
```

Alias позволяет открыть тот же route по другому path без redirect.

## Meta

```typescript
{
  path: "/admin",
  name: "admin",
  component: () => import("@/pages/AdminPage.vue"),
  meta: {
    requiresAuth: true,
    roles: ["admin"],
  },
}
```

`meta` удобно использовать в navigation guards.

## Мини-шпаргалка

- `path` описывает URL pattern.
- `name` удобно использовать для навигации.
- `component` показывает страницу.
- `props: true` передает params как props.
- `redirect` меняет URL.
- `alias` дает второй path для того же route.
- `meta` хранит route metadata.
