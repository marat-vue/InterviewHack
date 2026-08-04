# `Object.preventExtensions()`

> [!NOTE] Коротко
> `Object.preventExtensions(obj)` запрещает добавлять новые свойства в объект. Существующие свойства по-прежнему можно менять и удалять, если их дескрипторы это позволяют.

## Вопрос

Что делает `Object.preventExtensions()`?

## Базовый пример

```javascript
const user = {
  name: "Anna",
};

Object.preventExtensions(user);

user.age = 25; // не добавится
user.name = "Max"; // можно
delete user.name; // можно
```

В strict mode добавление нового свойства может дать `TypeError`.

## Проверка

```javascript
Object.isExtensible(user); // false
```

До вызова:

```javascript
Object.isExtensible({}); // true
```

## Что не меняется

`preventExtensions` не делает свойства readonly.

```javascript
const user = { name: "Anna" };

Object.preventExtensions(user);

user.name = "Max"; // можно
```

И не запрещает удаление:

```javascript
delete user.name; // можно
```

## Сравнение с `seal` и `freeze`

| Метод | Добавлять | Удалять | Менять значения |
| --- | --- | --- | --- |
| `preventExtensions` | нет | да | да |
| `seal` | нет | нет | да, если writable |
| `freeze` | нет | нет | нет |

## Мини-шпаргалка

```javascript
Object.preventExtensions(obj);
Object.isExtensible(obj); // false
```

| Операция | После `preventExtensions` |
| --- | --- |
| `obj.newKey = 1` | нельзя |
| `obj.oldKey = 2` | можно |
| `delete obj.oldKey` | можно |
| `Object.defineProperty(obj, "new", ...)` | нельзя |
