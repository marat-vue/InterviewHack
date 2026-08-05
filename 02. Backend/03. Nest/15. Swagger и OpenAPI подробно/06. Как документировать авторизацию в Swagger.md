# Как документировать авторизацию в Swagger?

> [!NOTE]
> Авторизацию в Swagger документируют через security schemes: Bearer token, cookies, API key и другие. В NestJS для JWT часто используют `addBearerAuth` в `DocumentBuilder` и `@ApiBearerAuth` на protected endpoints.

## Bearer auth setup

```ts
const config = new DocumentBuilder()
  .setTitle('App API')
  .addBearerAuth()
  .build();
```

## Endpoint

```ts
@ApiBearerAuth()
@UseGuards(JwtAuthGuard)
@Get('me')
getMe() {}
```

## Cookie auth

Для cookie-based session можно добавить API key через cookie.

```ts
const config = new DocumentBuilder()
  .addCookieAuth('better-auth.session_token')
  .build();
```

Конкретное имя cookie зависит от Better Auth config и cookie prefix.

## Ошибки auth

```ts
@ApiUnauthorizedResponse({ description: 'Unauthenticated' })
@ApiForbiddenResponse({ description: 'Not enough permissions' })
```

## Мини-шпаргалка

- `addBearerAuth` добавляет JWT security scheme.
- `@ApiBearerAuth` помечает protected route.
- Для cookies можно использовать `addCookieAuth`.
- 401 и 403 нужно документировать отдельно.
- Swagger auth scheme должен совпадать с реальной auth-схемой.
