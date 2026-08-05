# Как мониторить NestJS приложение?

> [!NOTE]
> Monitoring NestJS-приложения строится на logs, metrics, traces, health checks и алертах. Важно следить не только за ошибками, но и за latency, memory, event loop delay, database pool и queue lag.

## Health check

```ts
@Controller('health')
export class HealthController {
  @Get()
  check() {
    return { ok: true };
  }
}
```

Для production можно использовать `@nestjs/terminus`.

## Метрики

Полезно отслеживать:

- request duration;
- error rate;
- throughput;
- memory usage;
- CPU usage;
- event loop lag;
- DB query duration;
- queue size;
- external API latency.

## Tracing

Distributed tracing помогает понять путь запроса через NestJS API, database, queues и microservices.

## Мини-шпаргалка

- Health check нужен load balancer и orchestrator.
- Logs показывают события.
- Metrics показывают состояние во времени.
- Traces показывают путь запроса.
- Алерты должны быть по пользовательскому impact, не только по CPU.
