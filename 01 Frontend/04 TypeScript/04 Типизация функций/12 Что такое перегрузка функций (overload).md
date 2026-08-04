# Что такое перегрузка функций (overload)?

> [!NOTE] Коротко
> Перегрузка функций позволяет описать несколько вариантов вызова одной функции. Снаружи видны overload-сигнатуры, внутри пишется одна общая реализация.

## Вопрос

Что такое перегрузка функций?

## Синтаксис

```typescript
function parse(value: string): number;
function parse(value: number): string;
function parse(value: string | number): string | number {
  if (typeof value === "string") {
    return Number(value);
  }

  return String(value);
}
```

Первые две строки - сигнатуры вызова. Последняя функция - реальная реализация.

## Зачем это нужно

Overload полезен, когда тип результата зависит от типа или количества аргументов.

```typescript
function getValue(key: "id"): number;
function getValue(key: "name"): string;
function getValue(key: "id" | "name"): number | string {
  return key === "id" ? 1 : "Анна";
}

const id = getValue("id"); // number
const name = getValue("name"); // string
```

## Перегрузка по количеству аргументов

```typescript
function createUser(name: string): { name: string };
function createUser(name: string, age: number): { name: string; age: number };
function createUser(name: string, age?: number) {
  return age === undefined ? { name } : { name, age };
}
```

## Когда лучше без overload

Если логика одинаковая и результат не зависит от входа, чаще проще использовать union или generic.

```typescript
function wrap<T>(value: T): T[] {
  return [value];
}
```

## Мини-шпаргалка

- Сначала overload-сигнатуры, потом реализация.
- Реализация должна покрывать все варианты.
- Снаружи видны только overload-сигнатуры.
- Используй overload, когда вход влияет на точный тип результата.
