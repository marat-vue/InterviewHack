# Что такое navigation guard?

> [!NOTE] Коротко
> Navigation guard - проверка, которая выполняется до, во время или после перехода маршрута. Guards используют для авторизации, редиректов, подтверждения выхода и загрузки данных.

## Вопрос

Что такое `navigation guard`?

## Глобальный guard

```typescript
router.beforeEach((to, from) => {
  const isAuth = Boolean(localStorage.getItem("token"));

  if (to.meta.requiresAuth && !isAuth) {
    return { name: "login" };
  }
});
```

Если маршрут требует авторизации, guard может перенаправить пользователя.

## Meta поля маршрута

```typescript
{
  path: "/profile",
  name: "profile",
  component: ProfilePage,
  meta: { requiresAuth: true },
}
```

`meta` удобно использовать для правил доступа.

## Guard внутри компонента

```typescript
import { onBeforeRouteLeave } from "vue-router";

onBeforeRouteLeave(() => {
  return window.confirm("Уйти со страницы?");
});
```

Так можно предупредить пользователя о несохраненных изменениях.

## Что может вернуть guard

Guard может разрешить переход, отменить его, вернуть редирект или выбросить ошибку.

## Мини-шпаргалка

- Guard проверяет переход между маршрутами.
- `beforeEach` - глобальная проверка.
- `meta` хранит правила маршрута.
- `onBeforeRouteLeave` полезен для форм с несохраненными изменениями.
