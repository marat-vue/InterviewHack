# Что такое caching в NestJS?

> [!NOTE]
> Caching в NestJS можно реализовать через cache module/interceptor или вручную в services. Cache помогает ускорить чтение, но требует стратегии invalidation и понимания, какие данные можно кэшировать.

## Cache interceptor идея

```ts
@UseInterceptors(CacheInterceptor)
@Get()
findAll() {
  return this.productsService.findAll();
}
```

Interceptor может вернуть cached response вместо выполнения handler.

## Что кэшировать?

- публичные справочники;
- редко меняющиеся списки;
- expensive read queries;
- external API responses;
- computed reports.

## Что не кэшировать бездумно?

- персональные данные;
- ответы с правами доступа;
- данные с частыми изменениями;
- ошибки;
- sensitive payloads.

## Invalidation

Главный вопрос cache - не как положить значение, а когда его удалить или обновить.

## Мини-шпаргалка

- Cache ускоряет чтение.
- Cache может вернуть устаревшие данные.
- Interceptor удобен для response cache.
- Service-level cache дает больше контроля.
- Invalidation важнее самого механизма записи.
