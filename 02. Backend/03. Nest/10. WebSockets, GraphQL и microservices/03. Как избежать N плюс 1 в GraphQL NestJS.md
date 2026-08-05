# Как избежать N плюс 1 в GraphQL NestJS?

> [!NOTE]
> N+1 в GraphQL возникает, когда resolver для списка вызывает отдельный запрос к базе для каждого элемента. Обычно проблему решают DataLoader, batch loading, joins или заранее подготовленными queries.

## Проблема

```txt
Query users -> 1 запрос
User.posts для каждого user -> N запросов
```

## DataLoader идея

```ts
const postsByUserLoader = new DataLoader(async (userIds: readonly number[]) => {
  const posts = await postsRepository.findByUserIds(userIds);
  return userIds.map((id) => posts.filter((post) => post.userId === id));
});
```

DataLoader собирает много запросов в batch.

## Где хранить loader?

Loader обычно должен быть request-scoped, чтобы cache не смешивал данные разных пользователей и прав доступа.

## Мини-шпаргалка

- GraphQL легко провоцирует N+1.
- DataLoader делает batch loading.
- Loader cache должен быть per-request.
- Guards и permissions влияют на batching.
- SQL/ORM план все равно нужно понимать.
