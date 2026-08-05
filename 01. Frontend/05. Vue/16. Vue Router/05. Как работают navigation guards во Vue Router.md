# Как работают navigation guards во Vue Router?

> [!NOTE]
> Navigation guards позволяют разрешить, отменить или перенаправить переход. Их используют для auth, ролей, unsaved changes, redirects и аналитики навигации.

## Global beforeEach

```typescript
router.beforeEach((to) => {
  const authStore = useAuthStore();

  if (to.meta.requiresAuth && !authStore.isAuthenticated) {
    return {
      name: "login",
      query: { redirect: to.fullPath },
    };
  }
});
```

Если guard возвращает route location, Vue Router делает redirect. Если возвращает `false`, навигация отменяется.

## Role check

```typescript
router.beforeEach((to) => {
  const authStore = useAuthStore();
  const roles = to.meta.roles as string[] | undefined;

  if (roles && !roles.includes(authStore.user?.role ?? "")) {
    return { name: "forbidden" };
  }
});
```

Frontend guard нужен для UX, но backend все равно обязан проверять права на API.

## Per-route guard

```typescript
{
  path: "/admin",
  component: AdminPage,
  beforeEnter: (to) => {
    const authStore = useAuthStore();
    if (!authStore.isAdmin) return { name: "home" };
  },
}
```

## Component guards

Во Vue Router есть guards на уровне компонента, например для предупреждения о несохраненной форме:

```typescript
onBeforeRouteLeave(() => {
  if (hasUnsavedChanges.value) {
    return window.confirm("Уйти без сохранения?");
  }
});
```

## Частые ошибки

| Ошибка | Почему плохо |
|---|---|
| делать auth только на frontend guard | API остается незащищенным |
| не возвращать redirect из guard | навигация продолжится |
| делать бесконечный redirect на login | приложение зациклится |
| загружать тяжелые данные в каждом guard | навигация станет медленной |

## Мини-шпаргалка

- Guards управляют переходами.
- `beforeEach` срабатывает глобально.
- `beforeEnter` задается на route.
- `onBeforeRouteLeave` полезен для unsaved changes.
- Frontend guards не заменяют backend authorization.
- Redirect на login часто хранит `redirect=to.fullPath`.
