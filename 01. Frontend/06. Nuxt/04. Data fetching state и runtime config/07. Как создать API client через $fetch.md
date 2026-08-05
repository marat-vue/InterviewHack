# Как создать API client через $fetch?

> [!NOTE]
> В Nuxt часто создают custom `$fetch` client в plugin: задают `baseURL`, headers, auth handling и error handling. Для SSR initial data такой client лучше использовать внутри `useAsyncData`, чтобы избежать double fetch.

## Plugin

```ts
// app/plugins/api.ts
export default defineNuxtPlugin(() => {
  const config = useRuntimeConfig();

  const api = $fetch.create({
    baseURL: config.public.apiBase,
    onRequest({ options }) {
      const token = useCookie('access_token');

      if (token.value) {
        options.headers.set('Authorization', `Bearer ${token.value}`);
      }
    },
  });

  return {
    provide: {
      api,
    },
  };
});
```

## Использование в action

```ts
const { $api } = useNuxtApp();

async function logout() {
  await $api('/auth/logout', {
    method: 'POST',
  });
}
```

## Использование для SSR data

```ts
const { $api } = useNuxtApp();

const { data: profile } = await useAsyncData('profile', () => {
  return $api('/profile');
});
```

Так результат попадет в Nuxt payload.

## Error handling

```ts
const api = $fetch.create({
  baseURL: config.public.apiBase,
  async onResponseError({ response }) {
    if (response.status === 401) {
      await navigateTo('/login');
    }
  },
});
```

## Мини-шпаргалка

- `$fetch.create` создает custom client.
- `baseURL` удобно брать из `runtimeConfig.public`.
- Auth header можно добавлять в `onRequest`.
- Для SSR data используй `$api` внутри `useAsyncData`.
- Не клади secret tokens в `public` config.
