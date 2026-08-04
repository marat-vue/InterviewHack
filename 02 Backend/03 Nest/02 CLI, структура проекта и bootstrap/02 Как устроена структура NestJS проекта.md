# Как устроена структура NestJS проекта?

> [!NOTE]
> Типичный NestJS-проект содержит `main.ts`, корневой `AppModule`, feature modules, controllers, services, DTO, tests и конфигурационные файлы TypeScript, ESLint и package scripts.

## Базовая структура

```txt
src/
  main.ts
  app.module.ts
  users/
    users.module.ts
    users.controller.ts
    users.service.ts
    dto/
      create-user.dto.ts
test/
  app.e2e-spec.ts
```

## Роли файлов

| Файл | Роль |
|---|---|
| `main.ts` | bootstrap приложения |
| `app.module.ts` | корневой модуль |
| `*.module.ts` | feature module |
| `*.controller.ts` | HTTP routes |
| `*.service.ts` | бизнес-логика |
| `dto/*.dto.ts` | входные/выходные контракты |

## Что важно

Структура должна помогать навигации. Если модуль растет, внутри него можно выделять подпапки: `dto`, `entities`, `repositories`, `guards`, `strategies`.

## Мини-шпаргалка

- `main.ts` запускает приложение.
- `AppModule` собирает корневые imports.
- Feature modules хранят доменную логику.
- Controllers не должны содержать тяжелую бизнес-логику.
- DTO лучше держать рядом с модулем, где они используются.
