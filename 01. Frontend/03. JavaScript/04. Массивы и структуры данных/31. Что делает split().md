# `split()`

> [!NOTE]
> `split()` - метод строки, который разбивает строку на массив подстрок по указанному разделителю.

## Вопрос

Что делает `split()`?

## Пример

```javascript
const str = "apple,banana,cherry";

const arr = str.split(",");

console.log(arr); // ["apple", "banana", "cherry"]
```

Важно: это метод строки, не массива.

## Разделитель

```javascript
"a-b-c".split("-"); // ["a", "b", "c"]
"a b c".split(" "); // ["a", "b", "c"]
```

Разбить на символы:

```javascript
"hello".split(""); // ["h", "e", "l", "l", "o"]
```

## `limit`

Второй аргумент ограничивает количество элементов.

```javascript
"a,b,c".split(",", 2); // ["a", "b"]
```

## Если разделитель не найден

```javascript
"abc".split(","); // ["abc"]
```

## Связка `split` + `join`

```javascript
const normalized = "hello world"
  .split(" ")
  .join("-");

console.log(normalized); // "hello-world"
```

## Мини-шпаргалка

| Код | Результат |
| --- | --- |
| `"a,b".split(",")` | `["a", "b"]` |
| `"abc".split("")` | `["a", "b", "c"]` |
| `"abc".split(",")` | `["abc"]` |
| `"a,b,c".split(",", 2)` | `["a", "b"]` |
| `arr.join(",")` | обратная операция |
