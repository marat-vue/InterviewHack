# Почему NestJS не видит provider?

> [!NOTE]
> Ошибка "Nest can't resolve dependencies" обычно означает, что provider не зарегистрирован, не импортирован нужный module, не экспортирован provider из другого module или используется неправильный injection token.

## Типичная ошибка

```txt
Nest can't resolve dependencies of the OrdersService (?)
```

NestJS говорит: я создаю `OrdersService`, но одну из зависимостей в constructor не могу найти в DI container.

## Причина 1. Provider не зарегистрирован

```ts
@Module({
  providers: [OrdersService],
})
export class OrdersModule {}
```

Если `OrdersService` зависит от `UsersService`, но `UsersService` не доступен в module, будет ошибка.

## Причина 2. Module не импортирован

```ts
@Module({
  imports: [UsersModule],
  providers: [OrdersService],
})
export class OrdersModule {}
```

`OrdersModule` должен импортировать `UsersModule`.

## Причина 3. Provider не экспортирован

```ts
@Module({
  providers: [UsersService],
  exports: [UsersService],
})
export class UsersModule {}
```

Если `UsersService` нужен снаружи, `UsersModule` должен его export.

## Причина 4. Неправильный token

```ts
@Inject('USERS_REPOSITORY')
private readonly repository: UsersRepository;
```

Token в `@Inject()` должен совпадать с token в custom provider.

## Мини-шпаргалка

- Смотри constructor класса из ошибки.
- Проверь `providers` текущего module.
- Проверь `imports` текущего module.
- Проверь `exports` module, откуда берется provider.
- Проверь injection token.
