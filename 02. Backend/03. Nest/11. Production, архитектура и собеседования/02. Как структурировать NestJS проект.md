# Как структурировать NestJS проект?

> [!NOTE]
> NestJS-проект лучше структурировать по feature modules или доменным областям. Каждый module должен иметь понятную ответственность и не превращаться в свалку controllers, services и repositories.

## Feature-first структура

```txt
src/
  auth/
    auth.module.ts
    auth.controller.ts
    auth.service.ts
  users/
    users.module.ts
    users.controller.ts
    users.service.ts
    dto/
  orders/
    orders.module.ts
    orders.controller.ts
    orders.service.ts
```

## Shared и common

```txt
common/
  decorators/
  filters/
  guards/
  interceptors/
  pipes/
```

Не складывай туда бизнес-логику. `common` должен быть действительно общим.

## Infrastructure

```txt
database/
config/
logger/
queue/
```

Инфраструктура должна быть отделена от domain modules.

## Мини-шпаргалка

- Feature-first структура обычно понятнее.
- Module должен иметь четкую ответственность.
- `common` не должен стать мусорной папкой.
- Infrastructure dependencies лучше изолировать.
- Циклические зависимости - сигнал плохих границ.
