# Как получить текущего пользователя через custom decorator?

> [!NOTE]
> После успешной authentication guard обычно кладет пользователя в `request.user`. Чтобы не писать `@Req() req` в каждом controller, в NestJS удобно создать custom param decorator `@CurrentUser()`.

## Custom decorator

```ts
export const CurrentUser = createParamDecorator(
  (data: unknown, ctx: ExecutionContext) => {
    const request = ctx.switchToHttp().getRequest();
    return request.user;
  },
);
```

## Использование

```ts
@UseGuards(JwtAuthGuard)
@Get('me')
getMe(@CurrentUser() user: UserPayload) {
  return user;
}
```

## Получить поле пользователя

```ts
export const CurrentUser = createParamDecorator(
  (field: keyof UserPayload | undefined, ctx: ExecutionContext) => {
    const request = ctx.switchToHttp().getRequest();
    const user = request.user;

    return field ? user?.[field] : user;
  },
);
```

```ts
getMe(@CurrentUser('id') userId: string) {}
```

## Важный нюанс

Decorator только читает `request.user`. Он не должен сам проверять JWT. Проверка token - ответственность guard/strategy.

## Мини-шпаргалка

- Auth guard добавляет `request.user`.
- `@CurrentUser()` делает controller чище.
- Custom decorator создается через `createParamDecorator`.
- Проверка JWT остается в guard.
- Для GraphQL context decorator будет отличаться.
