# Что такое тип never?

> [!NOTE] Коротко
> `never` описывает значение, которое никогда не появится: функция не возвращает результат или ветка кода невозможна.

## Вопрос

Когда TypeScript использует тип `never`?

## Определение

`never` - нижний тип TypeScript. Он означает невозможное значение. Такой тип появляется, когда функция всегда выбрасывает ошибку, бесконечно выполняется или когда после narrowing не осталось допустимых вариантов.

## Функция, которая всегда бросает ошибку

```typescript
function fail(message: string): never {
  throw new Error(message);
}
```

Функция не возвращает управление нормальным способом.

## Бесконечный цикл

```typescript
function loop(): never {
  while (true) {}
}
```

Функция никогда не завершится.

## Exhaustive check

```typescript
type Status = 'idle' | 'loading' | 'success';

function render(status: Status): string {
  switch (status) {
    case 'idle':
      return 'Idle';
    case 'loading':
      return 'Loading';
    case 'success':
      return 'Success';
    default: {
      const exhaustiveCheck: never = status;
      return exhaustiveCheck;
    }
  }
}
```

Если в `Status` добавить новый вариант и забыть обработать его в `switch`, TypeScript покажет ошибку.

## never vs void

| Тип | Значение |
| --- | --- |
| `void` | функция завершилась, но ничего полезного не вернула |
| `never` | функция не завершилась нормальным образом |

## Мини-шпаргалка

```typescript
function fail(): never {
  throw new Error('failed');
}
```
