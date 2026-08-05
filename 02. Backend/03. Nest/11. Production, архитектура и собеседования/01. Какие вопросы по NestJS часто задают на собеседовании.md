# Какие вопросы по NestJS часто задают на собеседовании?

> [!NOTE]
> На собеседованиях по NestJS чаще всего проверяют архитектуру, DI, modules, request lifecycle, guards, pipes, interceptors, validation, error handling, testing, database layer и production-практики.

## Частые вопросы

| Тема | Вопрос |
|---|---|
| Архитектура | Чем NestJS отличается от Express? |
| Modules | Зачем нужны `imports` и `exports`? |
| DI | Что такое provider и injection token? |
| Lifecycle | В каком порядке идут middleware, guards, pipes, interceptors? |
| Validation | Как работает `ValidationPipe`? |
| Auth | Чем 401 отличается от 403? |
| Interceptors | Когда нужен interceptor? |
| Testing | Что такое `TestingModule`? |
| Production | Как сделать graceful shutdown? |

## Как отвечать

Хороший ответ:

- дает определение;
- показывает маленький пример;
- объясняет место в lifecycle;
- называет подводный камень;
- связывает с production-практикой.

## Мини-шпаргалка

- Обязательно знай request lifecycle.
- DI и modules - центр NestJS.
- Guards не то же самое, что middleware.
- Pipes работают до handler.
- Interceptors оборачивают handler и response.
