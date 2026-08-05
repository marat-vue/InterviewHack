# `Reflect`

> [!NOTE]
> `Reflect` - встроенный объект со статическими методами для низкоуровневых операций над объектами: чтение, запись, удаление, проверка свойств, вызов функций и создание экземпляров.

## Вопрос

Что делает `Reflect`?

## Основная идея

`Reflect` дает единый API для операций, которые обычно записываются разными синтаксисами.

```javascript
obj[key];              // обычное чтение
Reflect.get(obj, key); // то же через Reflect
```

```javascript
delete obj[key];                  // обычное удаление
Reflect.deleteProperty(obj, key); // через Reflect
```

## Частые методы

| Метод | Аналог |
| --- | --- |
| `Reflect.get(obj, key)` | `obj[key]` |
| `Reflect.set(obj, key, value)` | `obj[key] = value` |
| `Reflect.has(obj, key)` | `key in obj` |
| `Reflect.deleteProperty(obj, key)` | `delete obj[key]` |
| `Reflect.defineProperty(obj, key, desc)` | `Object.defineProperty` |
| `Reflect.apply(fn, thisArg, args)` | `fn.apply(thisArg, args)` |
| `Reflect.construct(Ctor, args)` | `new Ctor(...args)` |

## Пример с чтением и записью

```javascript
const user = { name: "Anna" };

Reflect.get(user, "name"); // "Anna"
Reflect.set(user, "age", 25); // true

console.log(user.age); // 25
```

Многие методы `Reflect` возвращают boolean, показывающий успех операции.

## С Proxy

`Reflect` особенно полезен внутри traps.

```javascript
const proxy = new Proxy(user, {
  get(target, prop, receiver) {
    console.log(`get ${String(prop)}`);
    return Reflect.get(target, prop, receiver);
  },

  set(target, prop, value, receiver) {
    console.log(`set ${String(prop)}`);
    return Reflect.set(target, prop, value, receiver);
  },
});
```

Так ловушка добавляет поведение, но не ломает стандартную механику.

## Почему важен `receiver`

`receiver` влияет на `this` в getter/setter при наследовании.

```javascript
Reflect.get(target, prop, receiver);
```

В большинстве простых случаев можно не углубляться, но в Proxy лучше передавать `receiver` дальше.

## Мини-шпаргалка

```javascript
Reflect.get(obj, "key");
Reflect.set(obj, "key", value);
Reflect.has(obj, "key");
Reflect.deleteProperty(obj, "key");
Reflect.apply(fn, thisArg, args);
Reflect.construct(Ctor, args);
```
