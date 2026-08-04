# Как логировать ошибки в NestJS?

> [!NOTE]
> Ошибки в NestJS логируют через built-in Logger, custom logger, exception filters или interceptors. В production логи должны быть структурированными, без секретов и с request id.

## Built-in Logger

```ts
private readonly logger = new Logger(UsersService.name);

this.logger.error('Failed to create user', error.stack);
```

## Exception filter

```ts
@Catch()
export class AllExceptionsFilter implements ExceptionFilter {
  private readonly logger = new Logger(AllExceptionsFilter.name);

  catch(exception: unknown, host: ArgumentsHost) {
    this.logger.error(exception);
  }
}
```

## Что добавлять в logs?

- request id;
- user id, если безопасно;
- route;
- status code;
- duration;
- error class;
- correlation id.

## Что не логировать?

- passwords;
- access tokens;
- refresh tokens;
- full cookies;
- private keys;
- raw personal data без необходимости.

## Мини-шпаргалка

- Production logs должны быть структурированными.
- Request id помогает расследовать баги.
- Filters хорошо подходят для error logging.
- Не отдавай stack trace клиенту.
- Не логируй secrets.
