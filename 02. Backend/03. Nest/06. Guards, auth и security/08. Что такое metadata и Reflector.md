# Что такое metadata и Reflector?

> [!NOTE]
> Metadata - данные, которые decorators прикрепляют к class или method. `Reflector` в NestJS помогает читать metadata внутри guards, interceptors и filters.

## SetMetadata

```ts
export const Public = () => SetMetadata('isPublic', true);
```

## Чтение metadata

```ts
@Injectable()
export class JwtAuthGuard extends AuthGuard('jwt') {
  constructor(private readonly reflector: Reflector) {
    super();
  }

  canActivate(context: ExecutionContext) {
    const isPublic = this.reflector.getAllAndOverride<boolean>('isPublic', [
      context.getHandler(),
      context.getClass(),
    ]);

    if (isPublic) return true;

    return super.canActivate(context);
  }
}
```

## Где применяется?

- public routes;
- roles;
- permissions;
- cache settings;
- custom serialization;
- throttling.

## Мини-шпаргалка

- Decorators могут сохранять metadata.
- `SetMetadata` задает metadata.
- `Reflector` читает metadata.
- `getHandler()` - method handler.
- `getClass()` - controller class.
