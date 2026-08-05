# void в функции

> [!NOTE]
> `void` у функции означает, что ее возвращаемое значение не должно использоваться. Такая функция выполняет действие, но не отдает значимый результат.

## Вопрос

Что означает возвращаемый тип `void` в функции?

## Основная идея

В JavaScript функция без `return` фактически возвращает `undefined`. В TypeScript `void` описывает не конкретное значение, а отсутствие полезного результата.

```typescript
function notify(message: string): void {
  console.log(message);
}

const result = notify("Готово");
// result имеет тип void, с ним нельзя нормально работать как со значением
```

## Где часто используется

`void` часто встречается в callback-типах, обработчиках событий и функциях с побочными эффектами.

```typescript
type ClickHandler = (event: MouseEvent) => void;

const handleClick: ClickHandler = (event) => {
  console.log(event.clientX);
};
```

## `void` и `undefined`

```typescript
function returnsUndefined(): undefined {
  return undefined;
}

function returnsVoid(): void {
  return;
}
```

`undefined` - конкретное значение. `void` - сигнал, что результат функции не важен.

## Частая ошибка

```typescript
function getName(): void {
  // return "Анна"; // ошибка: string не подходит для void
}
```

## Мини-шпаргалка

- `void` ставят функциям-действиям.
- Результат `void` не стоит использовать.
- Для callback часто пишут `() => void`.
- `void` не то же самое, что `never`.
