# Как работают nested routes, layouts, redirects и scrollBehavior?

> [!NOTE]
> Vue Router умеет строить вложенные интерфейсы через `children`, делать redirects, использовать layout routes и управлять прокруткой через `scrollBehavior`.

## Nested routes

```typescript
{
  path: "/users/:id",
  component: () => import("@/pages/users/UserLayout.vue"),
  children: [
    {
      path: "",
      name: "user-profile",
      component: () => import("@/pages/users/UserProfilePage.vue"),
    },
    {
      path: "orders",
      name: "user-orders",
      component: () => import("@/pages/users/UserOrdersPage.vue"),
    },
  ],
}
```

В `UserLayout.vue` нужен вложенный `RouterView`:

```vue
<template>
  <UserHeader />
  <RouterView />
</template>
```

## Layout routes

Можно сделать route без собственной страницы, который только задает layout:

```typescript
{
  path: "/admin",
  component: () => import("@/layouts/AdminLayout.vue"),
  meta: { requiresAuth: true },
  children: [
    { path: "users", component: () => import("@/pages/admin/UsersPage.vue") },
    { path: "settings", component: () => import("@/pages/admin/SettingsPage.vue") },
  ],
}
```

## Redirect

```typescript
{
  path: "/",
  redirect: "/dashboard",
}
```

Для старых URL:

```typescript
{
  path: "/profile",
  redirect: { name: "user-profile" },
}
```

## scrollBehavior

```typescript
export const router = createRouter({
  history: createWebHistory(),
  routes,
  scrollBehavior(to, from, savedPosition) {
    if (savedPosition) return savedPosition;
    if (to.hash) return { el: to.hash };
    return { top: 0 };
  },
});
```

Так можно возвращать scroll position при back/forward и прокручивать страницу вверх при обычной навигации.

## Мини-шпаргалка

- `children` создают nested routes.
- Parent component должен содержать `RouterView`.
- Layout route удобно использовать для admin/app/public зон.
- `redirect` переводит пользователя на другой route.
- `scrollBehavior` управляет прокруткой после навигации.
