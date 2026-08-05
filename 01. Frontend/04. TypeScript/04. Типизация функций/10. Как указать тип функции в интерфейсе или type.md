# Как указать тип функции в интерфейсе или type?

> [!NOTE]
> Функцию можно описать через `type`, через call signature в `interface` или как метод/поле объекта.

## Вопрос

Как указать тип функции в интерфейсе или `type`?

## Через `type`

Самая привычная запись для отдельной функции.

```typescript
type Formatter = (value: number) => string;

const formatPrice: Formatter = (value) => `${value} ₽`;
```

## Через `interface`

Интерфейс может описывать вызываемое значение.

```typescript
interface Formatter {
  (value: number): string;
}
```

Такой интерфейс означает: объект можно вызвать как функцию.

## Функция как поле объекта

```typescript
interface ButtonProps {
  label: string;
  onClick: (event: MouseEvent) => void;
}
```

## Метод объекта

```typescript
interface UserService {
  findById(id: number): Promise<User>;
  create(input: CreateUserInput): Promise<User>;
}
```

Записи `method(x: T): R` и `method: (x: T) => R` похожи, но для методов удобнее первая форма.

## Generic-функция

```typescript
type Mapper = <T, R>(items: T[], map: (item: T) => R) => R[];
```

## Мини-шпаргалка

- `type Fn = (x: T) => R` - отдельный тип функции.
- `interface Fn { (x: T): R }` - call signature.
- В объектах callback часто пишут как поле: `onClick: () => void`.
- Методы интерфейса обычно пишут как `method(arg: T): R`.
