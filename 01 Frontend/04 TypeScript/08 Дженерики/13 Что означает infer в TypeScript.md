# Что означает infer в TypeScript?

> [!NOTE] Коротко
> `infer` позволяет объявить временную переменную типа внутри conditional type и вывести ее из структуры другого типа.

## Вопрос

Что означает `infer` в TypeScript?

## Базовая идея

`infer` используется только внутри conditional types.

```typescript
type ElementType<T> = T extends Array<infer Item> ? Item : never;

type A = ElementType<string[]>;
// string
```

TypeScript смотрит на `Array<infer Item>` и выводит, что `Item` - это тип элемента массива.

## Достать return type

```typescript
type MyReturnType<T> = T extends (...args: any[]) => infer R ? R : never;

type Result = MyReturnType<() => number>;
// number
```

Так устроены многие встроенные utility-типы.

## Достать тип из Promise

```typescript
type UnwrapPromise<T> = T extends Promise<infer Value> ? Value : T;

type A = UnwrapPromise<Promise<User>>;
// User
```

## Почему это полезно

`infer` помогает не передавать тип руками, а получить его из уже существующей структуры.

## Мини-шпаргалка

- `infer` работает внутри `T extends Pattern ? ... : ...`.
- Он создает временное имя для найденного типа.
- Часто используется для массивов, функций, Promise и tuple.
- Если структура не совпала, срабатывает ветка `else`.
