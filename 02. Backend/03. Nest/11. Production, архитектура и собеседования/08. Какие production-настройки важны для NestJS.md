# Какие production-настройки важны для NestJS?

> [!NOTE]
> Production NestJS требует не только работающего controller. Нужны validation, CORS, security headers, rate limiting, timeouts, graceful shutdown, config validation, logs, health checks и безопасная работа с secrets.

## Checklist

| Настройка | Зачем |
|---|---|
| `ValidationPipe` | защита input |
| Config validation | раннее падение при плохом env |
| CORS allowlist | контроль browser origins |
| Rate limiting | защита auth endpoints |
| Helmet/security headers | базовая HTTP-защита |
| Shutdown hooks | корректная остановка |
| Health checks | orchestration |
| Structured logs | observability |

## main.ts

```ts
app.setGlobalPrefix('api');
app.enableCors({ origin: config.corsOrigins, credentials: true });
app.useGlobalPipes(new ValidationPipe({ whitelist: true, transform: true }));
app.enableShutdownHooks();
```

## Внешние вызовы

Все внешние API, database queries и microservice calls должны иметь timeout и понятную стратегию ошибок.

## Мини-шпаргалка

- Production начинается с config validation.
- Включай global validation.
- CORS должен быть ограниченным.
- Secrets не пишут в logs.
- Все distributed calls требуют timeout.
