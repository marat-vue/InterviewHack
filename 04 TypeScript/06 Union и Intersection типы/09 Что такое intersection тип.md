# Что такое intersection тип?

> [!NOTE] Коротко
> Intersection type объединяет требования нескольких типов. Запись `A & B` означает, что значение должно одновременно соответствовать и `A`, и `B`.

## Вопрос

Что такое intersection тип?

## Базовый пример

```typescript
type HasId = {
  id: string;
};

type HasTimestamps = {
  createdAt: Date;
  updatedAt: Date;
};

type Entity = HasId & HasTimestamps;

const entity: Entity = {
  id: "1",
  createdAt: new Date(),
  updatedAt: new Date(),
};
```

## Композиция объектных типов

Intersection удобен, когда один тип собирается из нескольких независимых частей.

```typescript
type ButtonProps = {
  label: string;
};

type WithAnalytics = {
  analyticsId: string;
};

type TrackedButtonProps = ButtonProps & WithAnalytics;
```

## Отличие от union

```typescript
type A = { a: string };
type B = { b: number };

type Union = A | B; // или a, или b
type Intersection = A & B; // и a, и b
```

## Конфликтующие поля

Если пересечь несовместимые поля, можно получить невозможный тип.

```typescript
type A = { id: string };
type B = { id: number };

type Broken = A & B;
// Broken["id"] будет never
```

## Мини-шпаргалка

- `A & B` - объект должен подходить под оба типа.
- Хорошо работает для композиции.
- Конфликт полей может привести к `never`.
- Для вариантов выбора нужен union, не intersection.
