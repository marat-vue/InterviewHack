# Как настроить global prefix и CORS?

> [!NOTE]
> Global prefix добавляет общий префикс ко всем маршрутам, например `/api`. CORS настраивает, какие браузерные origins могут обращаться к API из frontend-приложения.

## Global prefix

```ts
const app = await NestFactory.create(AppModule);

app.setGlobalPrefix('api');

await app.listen(3000);
```

Теперь `UsersController` с route `users` будет доступен как `/api/users`.

## CORS

```ts
app.enableCors({
  origin: ['https://app.example.com'],
  credentials: true,
});
```

Не стоит бездумно ставить `origin: true` или `*` для production API.

## Где настраивать?

Обычно global prefix и CORS настраивают в `main.ts`, потому что это поведение всего приложения.

## Мини-шпаргалка

- `setGlobalPrefix('api')` добавляет общий префикс.
- `enableCors()` включает CORS.
- Для credentials нельзя использовать wildcard origin.
- Production CORS должен быть ограниченным.
- Swagger path тоже стоит согласовать с prefix.
