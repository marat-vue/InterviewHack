# `Object.values()`

> [!NOTE] Коротко
> `Object.values(obj)` возвращает массив значений собственных перечисляемых свойств объекта.

## Вопрос

Что делает `Object.values()`?

## Базовый пример

```javascript
const user = {
  name: "Anna",
  age: 25,
};

Object.values(user); // ["Anna", 25]
```

Ключи в результат не попадают, только значения.

## Порядок значений

Порядок соответствует `Object.keys()` и `Object.entries()`.

```javascript
const obj = {
  a: 1,
  b: 2,
};

Object.keys(obj);   // ["a", "b"]
Object.values(obj); // [1, 2]
```

## Только собственные enumerable-свойства

```javascript
const proto = { role: "user" };
const user = Object.create(proto);
user.name = "Anna";

Object.values(user); // ["Anna"]
```

Унаследованные свойства не возвращаются.

Неперечисляемые тоже:

```javascript
Object.defineProperty(user, "id", {
  value: 1,
  enumerable: false,
});

Object.values(user); // ["Anna"]
```

## Практический пример

```javascript
const scores = {
  math: 90,
  english: 80,
  history: 70,
};

const average =
  Object.values(scores).reduce((sum, score) => sum + score, 0) /
  Object.values(scores).length;
```

## Мини-шпаргалка

| Метод | Для чего |
| --- | --- |
| `Object.keys(obj)` | получить ключи |
| `Object.values(obj)` | получить значения |
| `Object.entries(obj)` | получить пары |
| `Object.fromEntries(entries)` | собрать объект из пар |
