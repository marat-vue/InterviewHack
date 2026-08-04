# Что такое Set в TypeScript?

> [!NOTE] Коротко
> `Set<T>` - коллекция уникальных значений одного типа. Она хранит значения без повторов и удобна для проверки наличия элемента.

## Вопрос

Что такое `Set` в TypeScript?

## Базовый пример

```typescript
const ids = new Set<number>();

ids.add(1);
ids.add(2);
ids.add(1);

console.log(ids.size); // 2
```

Тип `Set<number>` означает, что в коллекцию можно добавлять только числа.

```typescript
// ids.add("3"); // ошибка
```

## Создание из массива

```typescript
const tags = ["ts", "js", "ts"];
const uniqueTags = new Set<string>(tags);
```

## Проверка наличия

```typescript
if (uniqueTags.has("ts")) {
  console.log("Тег уже есть");
}
```

## Перебор

```typescript
for (const tag of uniqueTags) {
  console.log(tag.toUpperCase());
}
```

## Set и объекты

Для объектов уникальность считается по ссылке, а не по содержимому.

```typescript
const users = new Set<object>();

users.add({ id: 1 });
users.add({ id: 1 });

console.log(users.size); // 2
```

## Мини-шпаргалка

- `Set<T>` хранит уникальные значения типа `T`.
- `add`, `has`, `delete`, `clear`, `size` - основные операции.
- Для примитивов уникальность очевидна, для объектов - по ссылке.
- Чтобы получить массив: `Array.from(mySet)`.

