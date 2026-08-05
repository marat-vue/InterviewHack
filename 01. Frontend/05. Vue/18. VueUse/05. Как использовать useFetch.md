# Как использовать useFetch?

> [!NOTE]
> `useFetch` из VueUse - reactive wrapper над Fetch API. Он помогает хранить `data`, `error`, loading-состояние, abort, refetch и создавать собственные fetch wrappers с базовыми options.

## Базовый пример

```typescript
import { useFetch } from "@vueuse/core";

const { data, error, isFetching } = useFetch("/api/users").json<User[]>();
```

В шаблоне:

```vue
<template>
  <p v-if="isFetching">Загрузка...</p>
  <p v-else-if="error">Ошибка</p>
  <UserList v-else :users="data ?? []" />
</template>
```

## POST

```typescript
const { data, error, execute } = useFetch("/api/users", {
  immediate: false,
})
  .post({ email: "anna@example.com" })
  .json<User>();

await execute();
```

## Interceptors

```typescript
const { data } = useFetch("/api/me", {
  beforeFetch({ options }) {
    options.headers = {
      ...options.headers,
      Authorization: `Bearer ${accessToken.value}`,
    };

    return { options };
  },
}).json<User>();
```

## Когда useFetch не хватает?

Для сложных server state сценариев часто лучше query library:

- cache;
- deduplication;
- retries;
- pagination;
- invalidation;
- optimistic updates.

`useFetch` хорош для простых запросов и composables, но не обязан заменять полноценный data fetching слой.

## Мини-шпаргалка

- `useFetch(url).json<T>()` возвращает reactive data/error/loading.
- `immediate: false` позволяет запускать request вручную.
- `execute` повторно запускает request.
- `beforeFetch` помогает добавить headers.
- Для сложного server cache нужен отдельный подход.
