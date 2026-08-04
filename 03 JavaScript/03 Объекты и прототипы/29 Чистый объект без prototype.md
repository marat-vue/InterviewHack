# Чистый объект без prototype

> [!NOTE] Коротко
> Чистый объект без прототипа создается через `Object.create(null)`. У него нет унаследованных методов вроде `toString` и `hasOwnProperty`.

## Вопрос

Как создать чистый объект без `Object.prototype`?

## Создание

```javascript
const dict = Object.create(null);

Object.getPrototypeOf(dict); // null
```

Такой объект не наследует от `Object.prototype`.

## Чем отличается от обычного объекта

```javascript
const obj = {};

obj.toString; // function
```

```javascript
const dict = Object.create(null);

dict.toString; // undefined
```

У `dict` нет `toString`, `constructor`, `hasOwnProperty` и других унаследованных свойств.

## Зачем нужен

Иногда такой объект используют как словарь, где не должно быть конфликтов с ключами из прототипа.

```javascript
const counts = Object.create(null);

counts.apple = 2;
counts.toString = 5; // обычный пользовательский ключ
```

В обычном объекте `toString` уже есть в прототипе.

## Подводные камни

Нельзя вызвать:

```javascript
dict.hasOwnProperty("apple"); // TypeError
```

Используйте:

```javascript
Object.hasOwn(dict, "apple");
```

Или:

```javascript
Object.prototype.hasOwnProperty.call(dict, "apple");
```

## В современном коде

Для словарей часто удобнее `Map`.

```javascript
const counts = new Map();

counts.set("apple", 2);
counts.get("apple"); // 2
```

## Мини-шпаргалка

| Объект | Прототип |
| --- | --- |
| `{}` | `Object.prototype` |
| `Object.create(null)` | `null` |
| `new Map()` | не объект-словарь, отдельная коллекция |
