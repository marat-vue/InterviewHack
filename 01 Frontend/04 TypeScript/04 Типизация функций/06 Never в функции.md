# Never в функции

> [!NOTE]
> Функция возвращает `never`, если она не может завершиться обычным способом: всегда выбрасывает ошибку, зацикливается или попадает в недостижимую ветку.

## Вопрос

В каком случае функция имеет тип возвращаемого значения `never`?

## Функция всегда бросает ошибку

```typescript
function fail(message: string): never {
  throw new Error(message);
}
```

После вызова такой функции выполнение не продолжается.

## Бесконечный цикл

```typescript
function runForever(): never {
  while (true) {
    // процесс не завершается
  }
}
```

## Exhaustive check

`never` часто используют, чтобы TypeScript проверял, что обработаны все варианты union.

```typescript
type Status = "idle" | "loading" | "success";

function renderStatus(status: Status): string {
  switch (status) {
    case "idle":
      return "Ожидание";
    case "loading":
      return "Загрузка";
    case "success":
      return "Готово";
    default: {
      const exhaustive: never = status;
      return exhaustive;
    }
  }
}
```

Если добавить новый статус, TypeScript подсветит `default`.

## `never` против `void`

`void` - функция завершилась, но ничего полезного не вернула. `never` - функция вообще не завершилась нормальным возвратом.

## Мини-шпаргалка

- `throw`-функции часто имеют `never`.
- Бесконечный цикл тоже дает `never`.
- `never` удобен для exhaustive check.
- `never` означает невозможное значение.
