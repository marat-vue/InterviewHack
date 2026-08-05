# Что такое route middleware?

> [!NOTE]
> Route middleware в Nuxt - код, который выполняется перед переходом на route. Его используют для auth, redirects, permissions, feature flags и проверки доступа к страницам.

## Пример auth middleware

```ts
// app/middleware/auth.ts
export default defineNuxtRouteMiddleware((to) => {
  const user = useState('user');

  if (!user.value) {
    return navigateTo(`/login?redirect=${to.fullPath}`);
  }
});
```

Подключение:

```vue
<script setup lang="ts">
definePageMeta({
  middleware: ['auth'],
});
</script>
```

## Global middleware

Файл с `.global` выполняется перед каждым route:

```text
app/middleware/analytics.global.ts
```

Пример:

```ts
export default defineNuxtRouteMiddleware((to) => {
  console.log('Navigate to', to.path);
});
```

## Inline middleware

```vue
<script setup lang="ts">
definePageMeta({
  middleware: defineNuxtRouteMiddleware(() => {
    const isFeatureEnabled = useFeatureFlag('new-dashboard');

    if (!isFeatureEnabled.value) {
      return navigateTo('/');
    }
  }),
});
</script>
```

## Что можно возвращать?

- `navigateTo('/login')` - redirect;
- `abortNavigation()` - отменить переход;
- ничего - разрешить переход.

## Мини-шпаргалка

- Route middleware выполняется перед route.
- Named middleware лежит в `app/middleware/name.ts`.
- Global middleware имеет suffix `.global`.
- Подключение через `definePageMeta`.
- Для server API middleware используется другая папка: `server/middleware`.
