# Как создать проект NestJS через CLI?

> [!NOTE]
> Nest CLI помогает создать проект, генерировать modules/controllers/services, запускать приложение, тесты и build. Это стандартный способ быстро начать NestJS-проект.

## Создание проекта

```bash
npm i -g @nestjs/cli
nest new app-name
```

CLI создаст структуру проекта, установит зависимости и подготовит стартовое приложение.

## Генерация ресурсов

```bash
nest generate module users
nest generate controller users
nest generate service users
```

Короткая форма:

```bash
nest g module users
nest g controller users
nest g service users
```

## Resource generator

```bash
nest g resource users
```

CLI может сгенерировать module, controller, service, DTO и базовые CRUD-файлы.

## Мини-шпаргалка

- CLI пакет: `@nestjs/cli`.
- Новый проект: `nest new`.
- Генерация: `nest g`.
- Resource generator полезен для CRUD.
- CLI помогает держать структуру однообразной.
