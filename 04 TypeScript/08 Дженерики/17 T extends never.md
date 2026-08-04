# T extends never

> [!NOTE] Коротко
> `T extends never` часто ведет себя неожиданно из-за дистрибутивности conditional types. Если `T` равен `never`, условие может вернуть тоже `never`, а не ожидаемые `true` или `false`.

## Вопрос

Что означает `T extends never`?

## Интуитивный пример

```typescript
type IsNever<T> = T extends never ? true : false;

type A = IsNever<string>;
// false

type B = IsNever<never>;
// never, а не true
```

Почему так? Conditional type распределяется по union. А `never` можно представить как пустой union, по которому нечего распределять.

## Правильная проверка на never

Чтобы отключить дистрибутивность, заворачивают `T` в tuple.

```typescript
type IsNever<T> = [T] extends [never] ? true : false;

type A = IsNever<string>;
// false

type B = IsNever<never>;
// true
```

## Где это встречается

Проверка на `never` нужна в advanced utility-типах, когда нужно обработать "пустой" результат вычислений.

```typescript
type FallbackIfNever<T, Fallback> = [T] extends [never] ? Fallback : T;

type Result = FallbackIfNever<Extract<"a", "b">, "none">;
// "none"
```

## Мини-шпаргалка

- `T extends never` с голым `T` дистрибутивен.
- Для `never` результат может стать `never`.
- Проверяй через `[T] extends [never]`.
- Это важный нюанс conditional types.
