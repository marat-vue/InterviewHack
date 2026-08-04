# Как проектировать repository layer в NestJS?

> [!NOTE]
> Repository layer скрывает детали хранения данных от business services. Он полезен, когда нужно отделить use cases от ORM, упростить тестирование и контролировать SQL/queries в одном месте.

## Без repository layer

```ts
@Injectable()
export class UsersService {
  constructor(private readonly prisma: PrismaService) {}

  findByEmail(email: string) {
    return this.prisma.user.findUnique({ where: { email } });
  }
}
```

Для маленького CRUD это нормально.

## С repository layer

```ts
@Injectable()
export class UsersRepository {
  constructor(private readonly prisma: PrismaService) {}

  findByEmail(email: string) {
    return this.prisma.user.findUnique({ where: { email } });
  }
}
```

Service зависит от repository, а не от Prisma напрямую.

## Когда нужен repository?

- сложные queries;
- несколько источников данных;
- частые mocks в тестах;
- domain-driven boundaries;
- желание скрыть ORM от business logic.

## Мини-шпаргалка

- Repository скрывает детали БД.
- Для простого CRUD можно не усложнять.
- Service должен выражать use case.
- Repository должен выражать data access.
- Абстракция нужна, когда реально снижает сложность.
