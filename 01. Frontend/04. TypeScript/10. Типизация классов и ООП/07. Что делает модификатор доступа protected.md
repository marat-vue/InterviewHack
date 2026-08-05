# Что делает модификатор доступа protected?

> [!NOTE]
> `protected` разрешает доступ внутри самого класса и его наследников, но запрещает обращаться к члену класса снаружи через экземпляр.

## Вопрос

Что делает модификатор доступа `protected`?

## Базовый пример

```typescript
class Animal {
  protected name: string;

  constructor(name: string) {
    this.name = name;
  }
}

class Dog extends Animal {
  bark(): string {
    return `${this.name} says woof`;
  }
}

const dog = new Dog("Rex");
// dog.name; // ошибка
```

## Когда использовать

`protected` полезен, когда базовый класс хранит детали, которые нужны наследникам, но не должны быть частью публичного API.

```typescript
abstract class ApiService {
  protected baseUrl = "/api";

  protected buildUrl(path: string): string {
    return `${this.baseUrl}${path}`;
  }
}
```

## Отличие от private

```typescript
class Base {
  private secret = "x";
  protected token = "y";
}

class Child extends Base {
  show() {
    // this.secret; // ошибка
    return this.token;
  }
}
```

## Мини-шпаргалка

- `protected` доступен классу и наследникам.
- Снаружи через экземпляр недоступен.
- Удобен для базовых классов.
- Если наследникам доступ не нужен, выбирай `private`.
