# Что такое provider и @Injectable?

> [!NOTE]
> Provider - объект, которым управляет NestJS DI container. `@Injectable()` помечает класс как provider, который можно внедрять в controllers, services и другие providers.

## Service как provider

```ts
@Injectable()
export class UsersService {
  findAll() {
    return [];
  }
}
```

Чтобы NestJS мог создать service, его регистрируют в module.

```ts
@Module({
  providers: [UsersService],
})
export class UsersModule {}
```

## Injection

```ts
@Controller('users')
export class UsersController {
  constructor(private readonly usersService: UsersService) {}
}
```

NestJS видит тип `UsersService` и внедряет экземпляр.

## Что может быть provider?

- service;
- repository;
- factory;
- helper;
- config;
- adapter;
- client внешнего API.

## Мини-шпаргалка

- Provider - управляемая DI-зависимость.
- `@Injectable()` помечает класс для DI.
- Provider нужно зарегистрировать в module.
- Внедрение обычно идет через constructor.
- Services не должны знать про HTTP напрямую.
