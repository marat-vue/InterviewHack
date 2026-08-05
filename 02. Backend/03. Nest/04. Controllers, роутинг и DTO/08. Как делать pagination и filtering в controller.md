# Как делать pagination и filtering в controller?

> [!NOTE]
> Pagination и filtering в NestJS обычно принимают через query DTO. Это позволяет валидировать page, limit, sort и фильтры так же, как body.

## Query DTO

```ts
export class FindUsersQueryDto {
  @IsOptional()
  @Type(() => Number)
  @IsInt()
  @Min(1)
  page = 1;

  @IsOptional()
  @Type(() => Number)
  @IsInt()
  @Min(1)
  @Max(100)
  limit = 20;
}
```

Controller:

```ts
@Get()
findAll(@Query() query: FindUsersQueryDto) {
  return this.usersService.findAll(query);
}
```

## Почему query DTO?

- единое место для правил;
- validation работает автоматически;
- легче документировать Swagger;
- меньше ручного parsing в controller.

## Мини-шпаргалка

- Query params тоже можно описывать DTO.
- Для чисел нужен transform.
- `limit` нужно ограничивать сверху.
- Sorting поля лучше проверять через allowlist.
- Controller передает query DTO в service.
