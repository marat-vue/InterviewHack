# Как документировать responses и auth в Swagger?

> [!NOTE]
> Swagger decorators позволяют явно описать status codes, response DTO, ошибки и auth requirements. Это делает API понятнее для frontend, QA и внешних клиентов.

## Response

```ts
@ApiOkResponse({ type: UserResponseDto })
@Get(':id')
findOne() {}
```

## Created response

```ts
@ApiCreatedResponse({ type: UserResponseDto })
@Post()
create() {}
```

## Auth

```ts
@ApiBearerAuth()
@UseGuards(JwtAuthGuard)
@Get('me')
getMe() {}
```

## Ошибки

```ts
@ApiNotFoundResponse({ description: 'User not found' })
@ApiBadRequestResponse({ description: 'Validation error' })
```

## Мини-шпаргалка

- Документируй успешные и ошибочные responses.
- `@ApiBearerAuth` показывает JWT requirement.
- Response DTO лучше делать явным.
- Swagger не должен расходиться с validation.
- Для публичного API документация - часть контракта.
