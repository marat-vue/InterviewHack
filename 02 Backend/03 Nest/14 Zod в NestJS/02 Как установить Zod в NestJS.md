# Как установить Zod в NestJS?

> [!NOTE]
> Для базового использования достаточно установить `zod`. Если нужно глубже интегрировать Zod с NestJS и Swagger, можно дополнительно использовать community-пакеты, но важно понимать базовый custom pipe.

## Установка

```bash
npm install zod
```

## Базовый импорт

```ts
import * as z from 'zod';
```

или:

```ts
import { z } from 'zod';
```

## Где хранить schemas?

Для feature module:

```txt
users/
  schemas/
    create-user.schema.ts
    find-users-query.schema.ts
  users.controller.ts
  users.service.ts
```

Если schemas общие для frontend/backend, их можно вынести в shared package.

## Мини-шпаргалка

- Основной пакет: `zod`.
- Schemas удобно хранить рядом с feature.
- Shared schemas можно вынести в отдельный package.
- NestJS сам по себе не применяет Zod без pipe.
- Для Swagger с Zod нужны дополнительные решения или ручное описание.
