# Как избежать N плюс 1 в NestJS?

> [!NOTE]
> N+1 возникает, когда приложение делает один запрос за списком и затем N запросов за связанными данными. В NestJS это часто появляется через ORM lazy loading, GraphQL field resolvers или неаккуратные service calls.

## Пример

```txt
GET /users
  -> SELECT users
  -> для каждого user SELECT orders
```

## Решения

- eager loading;
- explicit joins;
- batch loading;
- DataLoader для GraphQL;
- repository methods под конкретный use case;
- анализ SQL logs.

## В сервисе

Плохо:

```ts
for (const user of users) {
  user.orders = await this.ordersService.findByUserId(user.id);
}
```

Лучше:

```ts
const orders = await this.ordersRepository.findByUserIds(userIds);
```

## Мини-шпаргалка

- N+1 - много маленьких запросов вместо batch.
- ORM может скрывать проблему.
- GraphQL особенно уязвим к N+1.
- Batch loading часто лучше цикла с await.
- Проверяй реальные SQL queries.
