# Какие бывают injection scopes?

> [!NOTE]
> Injection scope определяет lifetime provider. По умолчанию providers в NestJS singleton, но можно использовать request scope или transient scope.

## Singleton scope

По умолчанию provider создается один раз и переиспользуется.

```ts
@Injectable()
export class UsersService {}
```

Это нормальный вариант для большинства сервисов.

## Request scope

```ts
@Injectable({ scope: Scope.REQUEST })
export class RequestContextService {}
```

Provider создается для каждого request.

## Transient scope

```ts
@Injectable({ scope: Scope.TRANSIENT })
export class FormatterService {}
```

Transient provider создает новый экземпляр для каждого consumer.

## Важный нюанс

Request scope может "поднимать" scope вверх по dependency graph: если controller зависит от request-scoped service, он тоже становится request-scoped. Это может влиять на производительность.

## Мини-шпаргалка

- Default scope - singleton.
- Request scope - новый экземпляр на request.
- Transient - новый экземпляр на consumer.
- Request scope дороже singleton.
- Не храни per-request state в singleton без явной модели.
