# Utility types для строк

> [!NOTE] Коротко
> TypeScript имеет встроенные строковые utility-типы: `Uppercase`, `Lowercase`, `Capitalize`, `Uncapitalize`. Они преобразуют string literal types на уровне типов.

## Вопрос

Какие есть utility-типы для строк?

## Основные типы

```typescript
type A = Uppercase<"admin">;
// "ADMIN"

type B = Lowercase<"USER">;
// "user"

type C = Capitalize<"profile">;
// "Profile"

type D = Uncapitalize<"Settings">;
// "settings"
```

Они работают именно с типами строковых литералов, а не с runtime-значениями.

## С union

```typescript
type Role = "admin" | "user";

type UpperRole = Uppercase<Role>;
// "ADMIN" | "USER"
```

## С template literal types

```typescript
type EventName = "click" | "submit";

type HandlerName = `on${Capitalize<EventName>}`;
// "onClick" | "onSubmit"
```

## Практический пример

```typescript
type Field = "name" | "email";
type GetterName = `get${Capitalize<Field>}`;

type Getters = Record<GetterName, () => string>;
```

## Мини-шпаргалка

- `Uppercase<S>` - переводит literal type в верхний регистр.
- `Lowercase<S>` - в нижний регистр.
- `Capitalize<S>` - первая буква в верхний регистр.
- `Uncapitalize<S>` - первая буква в нижний регистр.
