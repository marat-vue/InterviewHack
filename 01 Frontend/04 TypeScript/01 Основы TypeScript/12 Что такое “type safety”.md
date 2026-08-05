# Что такое “type safety”?

> [!NOTE]
> Type safety - свойство кода, при котором система типов не дает выполнять операции с неподходящими значениями.

## Вопрос

Что означает type safety в TypeScript?

## Определение

Type safety означает, что код защищен от ошибок несоответствия типов. Если функция ожидает число, TypeScript не позволит передать строку. Если объект может быть `null`, TypeScript заставит обработать этот случай.

## Пример

```typescript
function formatPrice(price: number) {
  return price.toFixed(2);
}

formatPrice(100);
formatPrice('100'); // ошибка TypeScript
```

## Null safety

```typescript
function printName(user: { name: string } | null) {
  if (user === null) {
    return;
  }

  console.log(user.name);
}
```

При `strictNullChecks` TypeScript не позволит обратиться к `user.name`, пока не исключен `null`.

## Где type safety особенно полезна

- параметры функций;
- ответы API;
- состояния UI;
- формы;
- reducers;
- публичные библиотеки;
- refactoring.

## Границы type safety

TypeScript проверяет код статически, но не валидирует автоматически данные в runtime.

```typescript
const user = await response.json() as User;
```

`as User` не проверяет данные, а только говорит компилятору доверять разработчику.

## Мини-шпаргалка

```text
type safety = fewer invalid operations with wrong values
```
