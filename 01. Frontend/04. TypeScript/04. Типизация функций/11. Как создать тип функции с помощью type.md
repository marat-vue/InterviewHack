# Как создать тип функции с помощью type?

> [!NOTE]
> `type` позволяет вынести сигнатуру функции в отдельное имя и переиспользовать ее в переменных, параметрах, объектах и callback-ах.

## Вопрос

Как создать тип функции с помощью `type`?

## Базовый синтаксис

```typescript
type FunctionName = (param: ParamType) => ReturnType;
```

Практический пример:

```typescript
type Compare = (a: number, b: number) => number;

const sortAsc: Compare = (a, b) => a - b;
```

## Callback

```typescript
type ChangeHandler = (value: string) => void;

function Input(props: { onChange: ChangeHandler }) {
  props.onChange("new value");
}
```

## Несколько параметров

```typescript
type CreateUser = (name: string, age?: number) => User;
```

## Rest-параметры

```typescript
type Join = (...parts: string[]) => string;

const join: Join = (...parts) => parts.join("/");
```

## Generic-функция

```typescript
type Identity = <T>(value: T) => T;

const identity: Identity = (value) => value;
```

## Мини-шпаргалка

- `type Fn = (...) => ...` - именованный тип функции.
- Удобно для callback-ов и публичных контрактов.
- Поддерживает optional, default, rest и generic-параметры.
- Если сигнатура используется один раз, можно писать inline.
