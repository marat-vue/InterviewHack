# Что такое WeakMap?

> [!NOTE]
> `WeakMap` - разновидность `Map`, где ключами могут быть только объекты, а ссылки на ключи являются слабыми.

## Вопрос

Зачем нужен `WeakMap` и почему его нельзя перебрать?

## Определение

`WeakMap` хранит пары "объект-ключ -> значение". Если объект-ключ больше нигде не используется, сборщик мусора может удалить его из памяти, а связанная запись в `WeakMap` исчезнет автоматически.

Это полезно для хранения служебных данных, которые не должны продлевать жизнь объектам.

## Пример

```javascript
const cache = new WeakMap();

let user = { id: 1, name: 'Ann' };

cache.set(user, { permissions: ['read'] });

console.log(cache.get(user)); // { permissions: ['read'] }
console.log(cache.has(user)); // true

user = null; // запись сможет исчезнуть после сборки мусора
```

## Ограничения

```javascript
const weakMap = new WeakMap();

weakMap.set({ id: 1 }, 'data'); // ok
// weakMap.set('id', 'data');   // TypeError
```

Ключи в `WeakMap` должны быть объектами. Значениями могут быть любые данные.

## Почему нет size и перебора

У `WeakMap` нет `size`, `keys()`, `values()`, `entries()` и `forEach()`. Причина в том, что наличие ключей зависит от сборщика мусора, а его работа не синхронизирована с вашим кодом.

## Где применяется

- приватные данные объекта;
- кэширование результатов для объектов;
- хранение метаданных DOM-элементов;
- защита от утечек памяти в долгоживущих коллекциях.

## Мини-шпаргалка

```javascript
const weakMap = new WeakMap();

weakMap.set(obj, value);
weakMap.get(obj);
weakMap.has(obj);
weakMap.delete(obj);
```
