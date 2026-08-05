# Что делает ключевое слово implements?

> [!NOTE]
> `implements` заставляет класс соответствовать интерфейсу или объектному типу. Это контракт на этапе компиляции: класс обязан иметь нужные свойства и методы.

## Вопрос

Что делает ключевое слово `implements`?

## Главная идея

`implements` не наследует код. Оно только проверяет форму класса: "в этом классе должны быть такие поля и методы".

```typescript
interface Printable {
  print(): void;
}

class Invoice implements Printable {
  print(): void {
    console.log("Печатаем счет");
  }
}
```

Если метод не реализовать, TypeScript покажет ошибку.

```typescript
class BrokenInvoice implements Printable {
  // ошибка: нет метода print
}
```

## Несколько интерфейсов

Класс может реализовать сразу несколько контрактов.

```typescript
interface Serializable {
  toJSON(): string;
}

class Report implements Printable, Serializable {
  print(): void {
    console.log("Отчет");
  }

  toJSON(): string {
    return "{}";
  }
}
```

## `implements` против `extends`

`extends` наследует реализацию от другого класса. `implements` только проверяет, что класс подходит под тип.

```typescript
class Animal {
  move() {}
}

interface Flyable {
  fly(): void;
}

class Bird extends Animal implements Flyable {
  fly(): void {}
}
```

## Важный нюанс

`implements` не меняет runtime-код. После компиляции в JavaScript от него ничего не остается.

## Мини-шпаргалка

- `implements` = класс выполняет контракт.
- Не дает готовую реализацию методов.
- Можно реализовать несколько интерфейсов.
- Используется только TypeScript-компилятором.
