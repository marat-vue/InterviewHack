# Что такое рекурсивный generic-тип?

> [!NOTE]
> Рекурсивный generic-тип ссылается сам на себя и при этом принимает параметр типа. Он нужен для деревьев, вложенных структур и deep-преобразований.

## Вопрос

Что такое рекурсивный generic-тип?

## Дерево значений

```typescript
type TreeNode<T> = {
  value: T;
  children?: TreeNode<T>[];
};

const tree: TreeNode<string> = {
  value: "root",
  children: [{ value: "child" }],
};
```

`T` сохраняется на всех уровнях дерева.

## Вложенное меню

```typescript
type MenuItem<TMeta = unknown> = {
  label: string;
  href: string;
  meta?: TMeta;
  children?: MenuItem<TMeta>[];
};
```

## Deep utility

```typescript
type DeepPartial<T> = {
  [K in keyof T]?: T[K] extends object ? DeepPartial<T[K]> : T[K];
};
```

Такой тип делает опциональными не только верхние поля, но и вложенные.

## Осторожно со сложностью

Слишком глубокая рекурсия может замедлить проверку типов или привести к ошибке "excessively deep".

## Мини-шпаргалка

- Рекурсивный generic содержит ссылку на себя: `Tree<T>`.
- Generic-параметр передается на следующий уровень.
- Подходит для деревьев и вложенных объектов.
- Deep utility-типы стоит писать осторожно.
