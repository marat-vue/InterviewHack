# Как работает ValidationPipe?

> [!NOTE]
> `ValidationPipe` проверяет входные данные по decorators из `class-validator` и может преобразовывать plain object в экземпляр DTO через `class-transformer`. Обычно его включают глобально.

## Глобальная настройка

```ts
app.useGlobalPipes(
  new ValidationPipe({
    whitelist: true,
    forbidNonWhitelisted: true,
    transform: true,
  }),
);
```

## DTO

```ts
export class CreateUserDto {
  @IsEmail()
  email: string;

  @IsString()
  @MinLength(2)
  name: string;
}
```

## Что делают опции?

| Опция | Что делает |
|---|---|
| `whitelist` | удаляет поля без decorators |
| `forbidNonWhitelisted` | выбрасывает ошибку за лишние поля |
| `transform` | преобразует plain object в DTO class |

## Мини-шпаргалка

- `ValidationPipe` - стандартный способ validation.
- Работает с DTO classes.
- `whitelist` защищает от лишних полей.
- `transform` помогает query/param преобразованиям.
- Включай validation на границе системы.
