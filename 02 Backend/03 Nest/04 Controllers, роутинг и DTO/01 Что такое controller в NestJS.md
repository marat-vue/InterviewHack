# Что такое controller в NestJS?

> [!NOTE]
> Controller принимает входящие HTTP-запросы и возвращает ответы клиенту. В NestJS controller описывается decorator `@Controller()` и содержит route handlers с decorators `@Get`, `@Post`, `@Patch`, `@Delete` и другими.

## Пример

```ts
@Controller('users')
export class UsersController {
  constructor(private readonly usersService: UsersService) {}

  @Get()
  findAll() {
    return this.usersService.findAll();
  }
}
```

Route будет доступен как `GET /users`.

## Роль controller

Controller должен:

- принять request;
- достать params/query/body;
- вызвать service;
- вернуть результат;
- не держать тяжелую бизнес-логику.

## Хорошая граница

```ts
@Post()
create(@Body() dto: CreateUserDto) {
  return this.usersService.create(dto);
}
```

Controller делегирует use case сервису.

## Мини-шпаргалка

- Controller обрабатывает HTTP routes.
- `@Controller('users')` задает route prefix.
- Методы помечаются `@Get`, `@Post` и т.д.
- Бизнес-логика должна быть в services.
- Controllers легко тестировать, если они тонкие.
