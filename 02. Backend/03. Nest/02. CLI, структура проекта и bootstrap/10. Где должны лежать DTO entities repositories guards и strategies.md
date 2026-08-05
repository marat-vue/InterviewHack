# Где должны лежать DTO, entities, repositories, guards и strategies?

> [!NOTE]
> В NestJS файлы лучше класть рядом с той фичей, которой они принадлежат. Общие infrastructure-компоненты можно держать в `common`, `config`, `database`, `auth`, но domain-specific файлы не стоит выносить в общий слой без причины.

## Feature-specific файлы

```txt
users/
  dto/
  entities/
  users.repository.ts
  users.service.ts
  users.controller.ts
  users.module.ts
```

Так проще понять, что относится к пользователям.

## Auth-specific файлы

```txt
auth/
  guards/
    jwt-auth.guard.ts
    roles.guard.ts
  strategies/
    jwt.strategy.ts
  decorators/
    current-user.decorator.ts
  auth.service.ts
  auth.module.ts
```

Auth guards и strategies обычно живут в `auth`, потому что это отдельная инфраструктурно-доменная область.

## Common

```txt
common/
  filters/
  interceptors/
  pipes/
  decorators/
```

В `common` стоит класть только действительно переиспользуемое.

## Мини-шпаргалка

- DTO фичи лежат в папке фичи.
- Entity/schema фичи часто лежит рядом с фичей или в database layer.
- Auth guards обычно лежат в `auth/guards`.
- Global filters/interceptors можно держать в `common`.
- Не превращай `common` в склад всего подряд.
