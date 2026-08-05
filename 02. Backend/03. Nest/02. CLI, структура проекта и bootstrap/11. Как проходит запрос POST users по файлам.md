# Как проходит запрос POST /users по файлам?

> [!NOTE]
> Запрос `POST /users` проходит через глобальные настройки, lifecycle-слои, controller, DTO validation, service и database layer. Этот путь помогает понять, зачем в NestJS столько файлов и как они связаны.

## Пример пути

```txt
main.ts
  -> AppModule
    -> UsersModule
      -> UsersController.create
        -> CreateUserDto + ValidationPipe
        -> UsersService.create
          -> UsersRepository или PrismaService
            -> Database
```

## main.ts

```ts
app.useGlobalPipes(new ValidationPipe({ whitelist: true, transform: true }));
```

Validation включается глобально.

## users.controller.ts

```ts
@Post()
create(@Body() dto: CreateUserDto) {
  return this.usersService.create(dto);
}
```

Controller принимает body и передает DTO в service.

## create-user.dto.ts

```ts
export class CreateUserDto {
  @IsEmail()
  email: string;

  @IsString()
  name: string;
}
```

DTO описывает правила входных данных.

## users.service.ts

```ts
async create(dto: CreateUserDto) {
  const exists = await this.usersRepository.findByEmail(dto.email);

  if (exists) {
    throw new ConflictException('Email already exists');
  }

  return this.usersRepository.create(dto);
}
```

Service выполняет use case и бизнес-проверки.

## Мини-шпаргалка

- `main.ts` включает глобальные правила.
- Module связывает controller и service.
- Controller принимает HTTP.
- DTO валидирует input.
- Service выполняет сценарий.
- Repository/ORM работает с БД.
