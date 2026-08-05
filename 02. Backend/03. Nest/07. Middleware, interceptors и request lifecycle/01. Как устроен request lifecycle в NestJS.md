# Как устроен request lifecycle в NestJS?

> [!NOTE]
> Request lifecycle в NestJS описывает порядок прохождения запроса через middleware, guards, interceptors, pipes, controller handler, exception filters и обратный путь response.

## Упрощенный порядок

```txt
request
  -> middleware
  -> guards
  -> interceptors before
  -> pipes
  -> controller handler
  -> service
  -> interceptors after
  -> response
```

Если возникает exception, его обрабатывает exception layer и filters.

## Почему порядок важен?

Guard не увидит результат pipe, потому что guard выполняется раньше pipes. Interceptor может обернуть выполнение handler, а pipe может не пустить request в handler при validation error.

## Типичный сценарий

- middleware добавляет request id;
- guard проверяет JWT;
- pipe валидирует DTO;
- controller вызывает service;
- interceptor логирует время ответа;
- filter форматирует ошибку.

## Мини-шпаргалка

- Middleware выполняется рано.
- Guards решают доступ.
- Interceptors оборачивают handler.
- Pipes валидируют и трансформируют аргументы.
- Filters обрабатывают exceptions.
