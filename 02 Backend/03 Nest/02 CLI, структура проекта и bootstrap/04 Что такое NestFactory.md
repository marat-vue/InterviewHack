# Что такое NestFactory?

> [!NOTE]
> `NestFactory` - класс, который создает экземпляр Nest-приложения из корневого модуля. Через него запускают HTTP-приложение, microservice или application context без HTTP-сервера.

## HTTP application

```ts
const app = await NestFactory.create(AppModule);
await app.listen(3000);
```

Это самый частый сценарий.

## Application context

Иногда Nest нужен без HTTP-сервера: CLI, worker, cron-like процесс.

```ts
const app = await NestFactory.createApplicationContext(AppModule);
const service = app.get(ReportsService);

await service.generate();
await app.close();
```

## Microservice

```ts
const app = await NestFactory.createMicroservice(AppModule, options);
await app.listen();
```

## Мини-шпаргалка

- `NestFactory` создает Nest runtime.
- `create` - HTTP-приложение.
- `createApplicationContext` - DI-контекст без HTTP.
- `createMicroservice` - microservice-приложение.
- Корневой модуль задает граф приложения.
