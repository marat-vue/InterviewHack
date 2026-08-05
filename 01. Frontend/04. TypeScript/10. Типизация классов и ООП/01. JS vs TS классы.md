# JS vs TS классы

> [!NOTE]
> Классы в TypeScript остаются JavaScript-классами, но получают типизацию полей, параметров конструктора, методов, модификаторов доступа, интерфейсов и generics.

## Вопрос

Чем отличаются классы в JavaScript и TypeScript?

## JavaScript-класс

```typescript
class User {
  constructor(name) {
    this.name = name;
  }

  greet() {
    return `Hi, ${this.name}`;
  }
}
```

В JavaScript типы параметров и полей не проверяются компилятором.

## TypeScript-класс

```typescript
class User {
  constructor(public name: string) {}

  greet(): string {
    return `Hi, ${this.name}`;
  }
}
```

TypeScript проверит, что `name` - строка, а `greet` возвращает строку.

## Что добавляет TypeScript

```typescript
class Account {
  private balance = 0;

  constructor(public readonly id: string) {}

  deposit(amount: number): void {
    this.balance += amount;
  }
}
```

Здесь есть типы, `private`, `readonly`, параметр-свойство и тип результата метода.

## Runtime и compile time

Большая часть TypeScript-конструкций исчезает после компиляции. Они нужны для проверки кода до запуска.

## Мини-шпаргалка

- TS-класс - это JS-класс плюс типы.
- Можно типизировать поля, конструктор и методы.
- Есть `public`, `private`, `protected`, `readonly`, `abstract`.
- Типы помогают проектировать контракт класса.
