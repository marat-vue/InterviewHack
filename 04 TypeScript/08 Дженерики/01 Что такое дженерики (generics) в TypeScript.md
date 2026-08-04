# Что такое дженерики (generics) в TypeScript?

> [!NOTE] Коротко
> Дженерики позволяют описывать типы с параметрами. Вместо одного конкретного типа функция, класс или интерфейс получают "переменную типа" и сохраняют связь между входом и выходом.

## Вопрос

Что такое дженерики в TypeScript?

## Простая идея

Generic - это способ сказать: "тип будет известен позже, но TypeScript должен помнить его".

```typescript
function identity<T>(value: T): T {
  return value;
}

const a = identity("hello"); // string
const b = identity(42); // number
```

`T` - параметр типа. Он подставляется при вызове.

## Зачем не `any`

```typescript
function identityAny(value: any): any {
  return value;
}

const result = identityAny("hello");
// result: any, TypeScript потерял информацию
```

Generic сохраняет точный тип, а `any` стирает проверку.

## Generic в типах

```typescript
type ApiResponse<T> = {
  data: T;
  status: number;
};

type UserResponse = ApiResponse<User>;
```

## Generic в интерфейсах

```typescript
interface Repository<T> {
  findById(id: string): Promise<T>;
  save(entity: T): Promise<void>;
}
```

## Мини-шпаргалка

- Generic = тип с параметром.
- `T` обычно означает "любой тип, но конкретный".
- Generic сохраняет связь между входом и выходом.
- Используется в функциях, типах, интерфейсах и классах.
