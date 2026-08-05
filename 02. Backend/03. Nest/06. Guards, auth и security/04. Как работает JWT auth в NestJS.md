# Как работает JWT auth в NestJS?

> [!NOTE]
> JWT auth обычно состоит из login endpoint, генерации access token, JWT strategy, guard и получения текущего пользователя из request. Token отправляют в `Authorization: Bearer ...`.

## Login flow

```txt
email/password -> AuthService.validateUser
  -> JwtService.sign
  -> access token
```

## Генерация token

```ts
const payload = { sub: user.id, email: user.email };

return {
  accessToken: await this.jwtService.signAsync(payload),
};
```

## Защищенный route

```ts
@UseGuards(JwtAuthGuard)
@Get('me')
getMe(@CurrentUser() user: CurrentUserDto) {
  return user;
}
```

## Важные решения

- срок жизни access token;
- refresh token стратегия;
- где хранить token на клиенте;
- как отзывать доступ;
- какие claims класть в payload.

## Мини-шпаргалка

- JWT подписывается secret/private key.
- В payload не кладут секреты.
- Access token должен жить ограниченное время.
- Guard проверяет token на каждом protected route.
- Refresh tokens требуют отдельной security-модели.
