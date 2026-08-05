# Что такое GraphQL resolver в NestJS?

> [!NOTE]
> GraphQL resolver в NestJS обрабатывает GraphQL queries, mutations и field resolvers. По роли он похож на controller, но работает не с REST routes, а с GraphQL schema.

## Resolver

```ts
@Resolver(() => User)
export class UsersResolver {
  constructor(private readonly usersService: UsersService) {}

  @Query(() => [User])
  users() {
    return this.usersService.findAll();
  }
}
```

## Mutation

```ts
@Mutation(() => User)
createUser(@Args('input') input: CreateUserInput) {
  return this.usersService.create(input);
}
```

## Code-first подход

NestJS часто используют с code-first GraphQL: TypeScript classes и decorators генерируют GraphQL schema.

## Resolver vs Controller

| REST | GraphQL |
|---|---|
| Controller | Resolver |
| Route | Query/Mutation |
| DTO | InputType/ObjectType |
| HTTP status | GraphQL response/errors |

## Мини-шпаргалка

- Resolver обрабатывает GraphQL operations.
- `@Query` читает данные.
- `@Mutation` изменяет данные.
- `@Args` получает аргументы.
- GraphQL требует особого внимания к N+1.
