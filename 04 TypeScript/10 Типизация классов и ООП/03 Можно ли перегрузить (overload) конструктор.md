# Можно ли перегрузить constructor?

> [!NOTE] Коротко
> Да, конструктор можно перегрузить: сначала пишут несколько сигнатур `constructor(...)`, а затем одну общую реализацию.

## Вопрос

Можно ли перегрузить (`overload`) конструктор?

## Базовый пример

```typescript
class User {
  name: string;
  age?: number;

  constructor(name: string);
  constructor(name: string, age: number);
  constructor(name: string, age?: number) {
    this.name = name;
    this.age = age;
  }
}

new User("Анна");
new User("Анна", 28);
```

Первые две строки - overload-сигнатуры. Последний `constructor` - реальная реализация.

## Реализация должна покрыть все варианты

```typescript
class Point {
  x: number;
  y: number;

  constructor(value: number);
  constructor(x: number, y: number);
  constructor(xOrValue: number, y?: number) {
    this.x = xOrValue;
    this.y = y ?? xOrValue;
  }
}
```

## Когда использовать

Overload конструктора полезен, когда объект можно создать несколькими понятными способами.

## Когда лучше не использовать

Если вариантов много, часто читаемее сделать статические factory-методы.

```typescript
class User {
  private constructor(public name: string) {}

  static fromName(name: string): User {
    return new User(name);
  }
}
```

## Мини-шпаргалка

- Перегрузка конструктора возможна.
- Сигнатуры идут перед реализацией.
- Реализация одна и должна обработать все варианты.
- При сложной логике подумай о factory-методах.
