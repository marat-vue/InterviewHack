# Что такое injection token?

> [!NOTE]
> Injection token - идентификатор зависимости в DI container. Обычно token - это class, но для interfaces, constants и внешних clients часто используют string или symbol.

## Class token

```ts
constructor(private readonly usersService: UsersService) {}
```

Здесь token - класс `UsersService`.

## String token

```ts
export const USERS_REPOSITORY = 'USERS_REPOSITORY';
```

```ts
@Injectable()
export class UsersService {
  constructor(
    @Inject(USERS_REPOSITORY)
    private readonly usersRepository: UsersRepository,
  ) {}
}
```

## Почему нужен token?

TypeScript interfaces исчезают в runtime, поэтому NestJS не может внедрить interface напрямую.

```ts
interface UsersRepository {}
```

Для такого контракта нужен явный token.

## Мини-шпаргалка

- Token идентифицирует provider.
- Class token работает автоматически.
- Interface не существует в runtime.
- Для interface-like зависимостей используй token.
- `symbol` снижает риск конфликтов string tokens.
