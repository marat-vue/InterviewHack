# Как использовать Prisma в service и repository?

> [!NOTE]
> В маленькой фиче service может использовать `PrismaService` напрямую. В более сложной фиче полезно выделить repository, чтобы business service не зависел от деталей Prisma-запросов.

## Прямо в service

```ts
@Injectable()
export class UsersService {
  constructor(private readonly prisma: PrismaService) {}

  findByEmail(email: string) {
    return this.prisma.user.findUnique({
      where: { email },
    });
  }
}
```

Для простого CRUD это нормально.

## Через repository

```ts
@Injectable()
export class UsersRepository {
  constructor(private readonly prisma: PrismaService) {}

  findByEmail(email: string) {
    return this.prisma.user.findUnique({ where: { email } });
  }
}
```

```ts
@Injectable()
export class UsersService {
  constructor(private readonly usersRepository: UsersRepository) {}
}
```

## Когда repository полезен?

- много сложных запросов;
- нужно мокать data access в тестах;
- service должен быть ближе к use cases;
- хочется скрыть ORM от domain logic;
- есть raw SQL или несколько источников данных.

## Мини-шпаргалка

- Для простого CRUD можно inject `PrismaService` в service.
- Для сложных запросов часто удобен repository.
- Controller не должен использовать Prisma напрямую.
- Repository не должен принимать HTTP request.
- Service отвечает за бизнес-сценарий.
