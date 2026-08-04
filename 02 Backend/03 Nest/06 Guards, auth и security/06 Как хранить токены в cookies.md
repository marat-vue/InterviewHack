# Как хранить токены в cookies?

> [!NOTE]
> Токены можно хранить в HttpOnly cookies, чтобы браузерный JavaScript не мог прочитать их напрямую. При этом нужно правильно настроить `Secure`, `SameSite`, CORS и CSRF-защиту.

## Set cookie

```ts
@Post('login')
async login(@Res({ passthrough: true }) res: Response) {
  const { accessToken } = await this.authService.login();

  res.cookie('access_token', accessToken, {
    httpOnly: true,
    secure: true,
    sameSite: 'lax',
  });

  return { ok: true };
}
```

## Важные флаги

| Флаг | Зачем |
|---|---|
| `HttpOnly` | JS не читает cookie |
| `Secure` | только HTTPS |
| `SameSite` | снижает CSRF-риски |
| `Max-Age` | срок жизни |

## CORS

Если frontend на другом origin и используются cookies, нужен `credentials: true` и точный origin.

## Мини-шпаргалка

- HttpOnly cookie защищает token от чтения через JS.
- `Secure` обязателен для production HTTPS.
- Cookies требуют внимания к CSRF.
- CORS с credentials не работает с wildcard origin.
- Храни refresh token осторожнее access token.
