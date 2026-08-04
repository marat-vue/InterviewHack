# readonly элементы

> [!NOTE] Коротко
> `readonly` у массива запрещает менять сам массив: нельзя присваивать элементы по индексу, делать `push`, `pop`, `splice` и другие мутации.

## Вопрос

Как объявить массив с `readonly` элементами?

## Две формы записи

```typescript
const ids: readonly number[] = [1, 2, 3];
const names: ReadonlyArray<string> = ["Анна", "Олег"];
```

Обе записи запрещают мутировать массив.

```typescript
// ids[0] = 10; // ошибка
// ids.push(4); // ошибка

const doubled = ids.map((id) => id * 2); // чтение и map разрешены
```

## Поверхностная неизменяемость

`readonly` защищает массив, но не обязательно объекты внутри него.

```typescript
const users: readonly { name: string }[] = [{ name: "Анна" }];

users[0].name = "Мария"; // разрешено: объект внутри не readonly
// users.push({ name: "Олег" }); // ошибка: массив readonly
```

Чтобы запретить изменение полей, нужно делать readonly и для объекта.

```typescript
type User = {
  readonly name: string;
};

const users: readonly User[] = [{ name: "Анна" }];
```

## `as const`

```typescript
const roles = ["admin", "user"] as const;
// тип: readonly ["admin", "user"]
```

`as const` делает литералы максимально узкими и readonly.

## Мини-шпаргалка

- `readonly T[]` - короткая запись.
- `ReadonlyArray<T>` - generic-запись.
- Мутирующие методы запрещены.
- Защита поверхностная, если элементы - объекты.
