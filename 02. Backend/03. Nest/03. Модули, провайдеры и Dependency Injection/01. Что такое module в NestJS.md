# Что такое module в NestJS?

> [!NOTE]
> Module - класс с decorator `@Module()`, который группирует controllers, providers и связи с другими modules. NestJS использует modules, чтобы организовать структуру приложения и область видимости зависимостей.

## Пример

```ts
@Module({
  imports: [],
  controllers: [UsersController],
  providers: [UsersService],
  exports: [UsersService],
})
export class UsersModule {}
```

## Поля @Module

| Поле | Что означает |
|---|---|
| `imports` | какие modules подключить |
| `controllers` | какие controllers принадлежат модулю |
| `providers` | какие providers доступны внутри |
| `exports` | что отдать другим modules |

## AppModule

`AppModule` - корневой модуль приложения. Он импортирует feature modules.

```ts
@Module({
  imports: [UsersModule, AuthModule],
})
export class AppModule {}
```

## Мини-шпаргалка

- Module группирует функциональность.
- `@Module()` передает metadata NestJS.
- Providers доступны внутри своего module.
- Чтобы использовать provider снаружи, его нужно export.
- Feature modules помогают держать проект понятным.
