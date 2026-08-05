# Какие production-настройки важны для Better Auth?

> [!NOTE]
> В production Better Auth требует сильный secret, корректный `baseURL`, trusted origins, HTTPS cookies, аккуратную работу за reverse proxy и понятную стратегию session expiration.

## Secret

```env
BETTER_AUTH_SECRET="long-random-secret"
```

Secret должен быть длинным, случайным и храниться как secret окружения. Better Auth поддерживает rotation через versioned secrets.

## Trusted origins

```ts
export const auth = betterAuth({
  trustedOrigins: [
    'https://app.example.com',
  ],
});
```

Не оставляй localhost в production allowlist.

## Cookies

Better Auth cookies в production должны быть `httpOnly` и `secure`. Если нужно менять имена или attributes cookies, это делается через advanced options.

## Reverse proxy

Если приложение стоит за proxy/load balancer, нужно правильно настроить forwarded headers и доверять только своим proxy, чтобы не открыть spoofing.

## Мини-шпаргалка

- Secret хранится только в env/secret manager.
- `trustedOrigins` должен быть строгим allowlist.
- Production cookies должны идти по HTTPS.
- За proxy важно доверять только своим headers.
- Session expiration и revocation нужно понимать заранее.
