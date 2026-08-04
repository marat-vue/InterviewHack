# Как валидировать env в NestJS?

> [!NOTE]
> Env validation проверяет обязательные переменные окружения при старте приложения. Это позволяет упасть сразу с понятной ошибкой, а не получить runtime-баг после деплоя.

## Validation через Joi

```ts
ConfigModule.forRoot({
  validationSchema: Joi.object({
    NODE_ENV: Joi.string().valid('development', 'production', 'test').required(),
    PORT: Joi.number().default(3000),
    DATABASE_URL: Joi.string().required(),
    JWT_SECRET: Joi.string().required(),
  }),
});
```

## Что проверять?

- обязательные secrets;
- URL базы данных;
- port;
- режим окружения;
- feature flags;
- лимиты и timeout.

## Типизация config

Для крупных проектов удобно делать config factory:

```ts
export default registerAs('database', () => ({
  url: process.env.DATABASE_URL,
}));
```

## Мини-шпаргалка

- Env validation должна выполняться при старте.
- Все env изначально строки.
- Не печатай secrets в logs.
- Для больших проектов полезен typed config.
- Config ошибки должны ломать запуск приложения.
