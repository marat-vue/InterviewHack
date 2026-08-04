# Как использовать Zod для env validation?

> [!NOTE]
> Zod можно использовать для проверки env-переменных при старте приложения. Это альтернатива Joi в `ConfigModule` и хороший способ получить typed config.

## Schema

```ts
const envSchema = z.object({
  NODE_ENV: z.enum(['development', 'test', 'production']),
  PORT: z.coerce.number().int().min(1).default(3000),
  DATABASE_URL: z.string().min(1),
  BETTER_AUTH_SECRET: z.string().min(32),
  BETTER_AUTH_URL: z.url(),
});
```

## Parse env

```ts
const env = envSchema.parse(process.env);

export const appConfig = {
  nodeEnv: env.NODE_ENV,
  port: env.PORT,
  databaseUrl: env.DATABASE_URL,
};
```

## В NestJS

Можно использовать Zod до `NestFactory.create` или внутри config factory.

```ts
ConfigModule.forRoot({
  isGlobal: true,
  validate: (config) => envSchema.parse(config),
});
```

## Мини-шпаргалка

- Env всегда приходит строками.
- `z.coerce.number()` полезен для PORT.
- Секреты проверяй на длину, но не логируй.
- Config validation должна ломать старт приложения.
- Typed config лучше, чем разбросанный `process.env`.
