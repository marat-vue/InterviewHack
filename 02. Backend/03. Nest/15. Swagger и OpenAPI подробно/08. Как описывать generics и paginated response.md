# Как описывать generics и paginated response?

> [!NOTE]
> TypeScript generics исчезают в runtime, поэтому Swagger не всегда может сам вывести `PaginatedDto<UserDto>`. Для таких случаев используют `@ApiExtraModels`, `getSchemaPath` и ручную schema-композицию.

## Paginated DTO идея

```ts
export class PaginatedDto<T> {
  items: T[];
  total: number;
  page: number;
  limit: number;
}
```

В runtime `T` недоступен, поэтому Swagger нужна помощь.

## Custom decorator

```ts
export const ApiPaginatedResponse = (model: Type<unknown>) =>
  applyDecorators(
    ApiExtraModels(PaginatedDto, model),
    ApiOkResponse({
      schema: {
        allOf: [
          { $ref: getSchemaPath(PaginatedDto) },
          {
            properties: {
              items: {
                type: 'array',
                items: { $ref: getSchemaPath(model) },
              },
            },
          },
        ],
      },
    }),
  );
```

## Использование

```ts
@ApiPaginatedResponse(UserDto)
@Get()
findAll() {}
```

## Мини-шпаргалка

- Generics стираются в runtime.
- Swagger не понимает `T` автоматически.
- `ApiExtraModels` регистрирует дополнительные модели.
- `getSchemaPath` дает `$ref`.
- Для pagination удобно сделать custom decorator.
