# Чем implements отличается от extends в классах?

> [!NOTE]
> `extends` наследует класс и его реализацию, а `implements` только проверяет, что класс соответствует интерфейсу или типу.

## Вопрос

Чем `implements` отличается от `extends` в классах?

## `extends`

`extends` создает наследование между классами.

```typescript
class Animal {
  move(): void {
    console.log("move");
  }
}

class Dog extends Animal {}

new Dog().move();
```

Наследник получает методы и свойства базового класса.

## `implements`

`implements` задает контракт, но не дает готового кода.

```typescript
interface Movable {
  move(): void;
}

class Robot implements Movable {
  move(): void {
    console.log("move");
  }
}
```

Метод нужно написать самому.

## Вместе

```typescript
interface Flyable {
  fly(): void;
}

class Bird extends Animal implements Flyable {
  fly(): void {
    console.log("fly");
  }
}
```

Класс может наследовать один класс и реализовать несколько интерфейсов.

## Мини-шпаргалка

- `extends` = наследование реализации.
- `implements` = проверка контракта.
- Класс может `extends` только один класс.
- Класс может `implements` несколько интерфейсов.
