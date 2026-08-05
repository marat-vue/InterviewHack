# Как использовать HttpException?

> [!NOTE]
> `HttpException` и готовые HTTP exceptions позволяют явно вернуть клиенту ошибку с нужным status code. В NestJS есть built-in классы вроде `NotFoundException`, `BadRequestException`, `ForbiddenException`.

## Built-in exception

```ts
throw new NotFoundException('User not found');
```

NestJS вернет HTTP 404.

## Другие частые exceptions

| Exception | Status |
|---|---|
| `BadRequestException` | 400 |
| `UnauthorizedException` | 401 |
| `ForbiddenException` | 403 |
| `NotFoundException` | 404 |
| `ConflictException` | 409 |
| `InternalServerErrorException` | 500 |

## Custom HttpException

```ts
throw new HttpException(
  { message: 'Custom error' },
  HttpStatus.BAD_REQUEST,
);
```

## Где бросать ошибки?

Service может бросить domain/application exception, а controller/filter превратить ее в HTTP-response. Для простых CRUD часто используют built-in HTTP exceptions прямо в service.

## Мини-шпаргалка

- HTTP exceptions формируют error response.
- Используй готовые classes для стандартных ошибок.
- 401 - не аутентифицирован.
- 403 - аутентифицирован, но нет прав.
- 409 хорошо подходит для conflict, например duplicate email.
