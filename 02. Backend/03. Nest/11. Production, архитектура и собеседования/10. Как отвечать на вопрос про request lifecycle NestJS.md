# Как отвечать на вопрос про request lifecycle NestJS?

> [!NOTE]
> На собеседовании request lifecycle нужно объяснять как последовательность слоев: middleware, guards, interceptors, pipes, handler, обратный путь interceptors и exception filters при ошибках.

## Короткий ответ

```txt
middleware -> guards -> interceptors before -> pipes
  -> controller handler -> service
  -> interceptors after -> response
```

Если где-то возникает exception, она идет в exception layer и может быть обработана filter.

## Что уточнить

- middleware не знает metadata handler;
- guard решает доступ;
- pipe валидирует аргументы handler;
- interceptor оборачивает handler;
- filter форматирует ошибку.

## Частая ловушка

Guard выполняется до pipe, поэтому guard не должен рассчитывать на уже провалидированный DTO body.

## Хороший пример ответа

Если пришел `POST /users`, сначала сработает middleware, затем auth/roles guards, потом interceptor до handler, затем ValidationPipe проверит `CreateUserDto`, controller вызовет service, response пройдет через interceptor обратно. Ошибки поймает exception layer/filter.

## Мини-шпаргалка

- Это один из главных вопросов по NestJS.
- Обязательно назови порядок.
- Объясни роль каждого слоя.
- Упомяни exception filters.
- Приведи пример с validation и auth.
