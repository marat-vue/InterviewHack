# Как защищать маршруты через Better Auth?

> [!NOTE]
> Nest integration для Better Auth регистрирует auth guard глобально: routes защищены по умолчанию, а публичные endpoints помечают `@AllowAnonymous()`. Session можно получить через `@Session()`.

## Получить session

```ts
import { Controller, Get } from '@nestjs/common';
import { Session, UserSession } from '@thallesp/nestjs-better-auth';

@Controller('users')
export class UsersController {
  @Get('me')
  getMe(@Session() session: UserSession) {
    return { user: session.user };
  }
}
```

## Публичный route

```ts
import { AllowAnonymous } from '@thallesp/nestjs-better-auth';

@AllowAnonymous()
@Get('public')
getPublic() {
  return { ok: true };
}
```

## Optional auth

```ts
import { OptionalAuth } from '@thallesp/nestjs-better-auth';

@OptionalAuth()
@Get('feed')
getFeed(@Session() session?: UserSession) {
  return this.feedService.findFor(session?.user);
}
```

## Мини-шпаргалка

- Better Auth integration защищает routes глобально.
- `@AllowAnonymous()` открывает публичный route.
- `@OptionalAuth()` позволяет session быть optional.
- `@Session()` достает session.
- Authorization все равно нужно проектировать отдельно.
