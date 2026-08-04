# Что такое middleware в NestJS?

> [!NOTE]
> Middleware выполняется до guards и route handler. Она похожа на Express middleware и подходит для задач уровня request: logging, request id, cookie parsing, простая предварительная обработка.

## Function middleware

```ts
export function logger(req: Request, res: Response, next: NextFunction) {
  console.log(req.method, req.url);
  next();
}
```

## Class middleware

```ts
@Injectable()
export class LoggerMiddleware implements NestMiddleware {
  use(req: Request, res: Response, next: NextFunction) {
    console.log(req.method, req.url);
    next();
  }
}
```

## Подключение

```ts
export class AppModule implements NestModule {
  configure(consumer: MiddlewareConsumer) {
    consumer.apply(LoggerMiddleware).forRoutes('*');
  }
}
```

## Middleware vs guard

Middleware не знает, какой handler будет вызван, а guard имеет `ExecutionContext` и может читать metadata route.

## Мини-шпаргалка

- Middleware выполняется рано.
- Нужно вызвать `next()`.
- Подходит для request id и logging.
- Для authorization обычно лучше guard.
- Class middleware поддерживает DI.
