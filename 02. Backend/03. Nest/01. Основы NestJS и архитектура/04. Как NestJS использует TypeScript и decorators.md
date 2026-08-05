# Как NestJS использует TypeScript и decorators?

> [!NOTE]
> NestJS активно использует TypeScript decorators для описания metadata: какие классы являются modules, controllers, providers, какие методы обрабатывают routes и какие параметры нужно взять из request.

## Пример decorators

```ts
@Controller('users')
export class UsersController {
  @Get(':id')
  findOne(@Param('id') id: string) {
    return { id };
  }
}
```

Здесь decorators описывают:

- `@Controller('users')` - route prefix;
- `@Get(':id')` - HTTP route;
- `@Param('id')` - взять параметр пути.

## Metadata

Decorators не просто украшают код. Они сохраняют metadata, которую NestJS читает при запуске приложения и использует для построения routing и DI-графа.

## Почему TypeScript важен?

TypeScript помогает:

- описывать DTO;
- типизировать сервисы;
- безопасно внедрять зависимости;
- документировать контракты;
- находить ошибки до runtime.

## Мини-шпаргалка

- NestJS heavily relies on decorators.
- Decorators добавляют metadata.
- `@Controller`, `@Injectable`, `@Module` - ключевые decorators.
- TypeScript делает контракты приложения явными.
- DTO-классы важны для validation и Swagger.
