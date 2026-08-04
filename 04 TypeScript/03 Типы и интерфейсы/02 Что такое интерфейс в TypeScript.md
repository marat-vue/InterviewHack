# Что такое интерфейс в TypeScript?

> [!NOTE] Коротко
> `interface` описывает структуру объекта: какие свойства и методы должны быть у значения.

## Вопрос

Что такое интерфейс в TypeScript?

## Определение

Интерфейс задает контракт для объекта. Он говорит TypeScript, какие поля, методы и их типы ожидаются.

Интерфейсы часто используют для описания DTO, props, моделей данных, классов и публичных API.

## Пример

```typescript
interface User {
  id: number;
  name: string;
  email?: string;
}

const user: User = {
  id: 1,
  name: 'Ann',
};
```

`email` опционален, потому что после имени стоит `?`.

## Метод в интерфейсе

```typescript
interface Logger {
  log(message: string): void;
}
```

Объект, соответствующий `Logger`, должен иметь метод `log`.

## Наследование интерфейсов

```typescript
interface Admin extends User {
  permissions: string[];
}
```

`Admin` получает поля `User` и добавляет свои.

## Почему интерфейсы удобны для объектов

- читаемый синтаксис;
- поддерживают `extends`;
- поддерживают declaration merging;
- хорошо подходят для классов через `implements`;
- естественно описывают форму объекта.

## Мини-шпаргалка

```typescript
interface Entity {
  id: number;
  name: string;
}
```
