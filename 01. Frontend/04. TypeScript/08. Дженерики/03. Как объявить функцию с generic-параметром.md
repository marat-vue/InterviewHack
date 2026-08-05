# Как объявить функцию с generic-параметром?

> [!NOTE]
> Generic-параметр функции объявляют перед списком аргументов: `function fn<T>(value: T): T`. `T` можно использовать в параметрах, результате и теле типа.

## Вопрос

Как объявить функцию с generic-параметром?

## Function declaration

```typescript
function wrap<T>(value: T): T[] {
  return [value];
}

const numbers = wrap(10); // number[]
const strings = wrap("ts"); // string[]
```

## Arrow function

```typescript
const wrap = <T>(value: T): T[] => {
  return [value];
};
```

В `.tsx` иногда добавляют запятую, чтобы не спутать generic с JSX.

```typescript
const identity = <T,>(value: T): T => value;
```

## Несколько использований одного `T`

```typescript
function getProperty<T, K extends keyof T>(object: T, key: K): T[K] {
  return object[key];
}
```

Здесь `K` зависит от ключей `T`, а результат зависит от выбранного ключа.

## Явное указание типа

Обычно TypeScript выводит generic сам, но тип можно указать руками.

```typescript
const value = wrap<string>("hello");
```

## Мини-шпаргалка

- `function fn<T>(value: T): T` - базовая форма.
- В стрелках: `const fn = <T,>(value: T) => value`.
- TypeScript часто выводит `T` по аргументам.
- Generic можно ограничить через `extends`.
