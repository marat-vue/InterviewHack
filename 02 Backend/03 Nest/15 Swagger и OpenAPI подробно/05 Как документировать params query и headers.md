# Как документировать params, query и headers?

> [!NOTE]
> Nest Swagger частично читает `@Param`, `@Query` и `@Body`, но для ясной документации часто используют decorators `@ApiParam`, `@ApiQuery` и `@ApiHeader`.

## Path params

```ts
@ApiParam({
  name: 'id',
  type: String,
  description: 'User id',
})
@Get(':id')
findOne(@Param('id') id: string) {}
```

## Query params

```ts
@ApiQuery({ name: 'page', required: false, example: 1 })
@ApiQuery({ name: 'limit', required: false, example: 20 })
@Get()
findAll() {}
```

## Headers

```ts
@ApiHeader({
  name: 'x-request-id',
  required: false,
  description: 'Request correlation id',
})
@Get()
findAll() {}
```

## Query DTO

Для сложных query params можно использовать DTO class и `@Query() query: FindUsersQueryDto`, но отдельные `@ApiQuery` иногда дают более точный контроль.

## Мини-шпаргалка

- `@ApiParam` документирует path param.
- `@ApiQuery` документирует query param.
- `@ApiHeader` документирует header.
- Для pagination нужны `page`, `limit`, `sort`.
- Документация должна совпадать с validation pipe.
