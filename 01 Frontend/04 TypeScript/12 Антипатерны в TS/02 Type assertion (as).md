# Type assertion (as)

> [!NOTE]
> `as` не проверяет значение и не преобразует его. Это утверждение для компилятора: "считай это таким типом". Из-за этого `as` легко скрывает ошибку.

## Вопрос

Почему `type assertion` через `as` может быть антипаттерном?

## Что делает `as`

```typescript
const value = document.querySelector("#app") as HTMLDivElement;
```

TypeScript поверит, что `value` - `HTMLDivElement`. Но если элемента нет, на runtime там будет `null`.

```typescript
value.innerText = "Hello"; // может упасть
```

## Плохой пример

```typescript
type User = {
  id: number;
  name: string;
};

const user = JSON.parse("{}") as User;

console.log(user.name.toUpperCase()); // runtime-ошибка
```

`as User` не проверил, что поле `name` действительно существует.

## Лучше: проверка или guard

```typescript
function isUser(value: unknown): value is User {
  return (
    typeof value === "object" &&
    value !== null &&
    "id" in value &&
    "name" in value
  );
}

const data: unknown = JSON.parse("{}");

if (isUser(data)) {
  console.log(data.name);
}
```

## Когда `as` уместен

`as` нормален, когда ты знаешь больше TypeScript и это знание подтверждено кодом: например, после проверки DOM-элемента или при работе с ограничениями внешней библиотеки.

```typescript
const element = document.querySelector("#app");

if (element instanceof HTMLDivElement) {
  element.innerText = "Hello";
}
```

## Мини-шпаргалка

- `as` не меняет значение на runtime.
- `as` не валидирует данные.
- Часто лучше narrowing, guard или runtime-валидация.
- Избегай двойного `as unknown as Type` без очень веской причины.
