# Ловушки Proxy

> [!NOTE]
> Ловушки (traps) - методы объекта `handler` в `new Proxy(target, handler)`, которые перехватывают операции над объектом: чтение, запись, удаление, проверку `in`, перечисление ключей и другие.

## Вопрос

Что такое ловушки (traps)?

## Базовая идея

```javascript
const proxy = new Proxy(target, handler);
```

`handler` содержит методы-ловушки. Если ловушка описана, JavaScript вызывает ее вместо стандартного поведения.

```javascript
const user = { name: "Anna" };

const proxy = new Proxy(user, {
  get(target, prop) {
    console.log(`Читаем ${String(prop)}`);
    return target[prop];
  },
});

proxy.name; // "Anna"
```

## Частые ловушки

| Trap | Что перехватывает |
| --- | --- |
| `get` | чтение `obj.prop` |
| `set` | запись `obj.prop = value` |
| `has` | оператор `in` |
| `deleteProperty` | `delete obj.prop` |
| `ownKeys` | `Object.keys`, `Reflect.ownKeys` |
| `apply` | вызов функции |
| `construct` | вызов через `new` |

## `set`

```javascript
const user = {};

const proxy = new Proxy(user, {
  set(target, prop, value) {
    if (prop === "age" && value < 0) {
      throw new Error("Возраст не может быть отрицательным");
    }

    target[prop] = value;
    return true;
  },
});

proxy.age = 25;
```

`set` должен вернуть `true`, если запись успешна.

## С `Reflect`

В ловушках часто используют `Reflect`, чтобы сохранить стандартное поведение и добавить свою логику.

```javascript
const proxy = new Proxy(user, {
  get(target, prop, receiver) {
    console.log(prop);
    return Reflect.get(target, prop, receiver);
  },
});
```

## Зачем нужны traps

- валидация данных;
- логирование операций;
- защита полей;
- реактивность;
- виртуальные свойства;
- метапрограммирование.

## Мини-шпаргалка

```javascript
new Proxy(target, {
  get(target, prop, receiver) {},
  set(target, prop, value, receiver) {},
  has(target, prop) {},
  deleteProperty(target, prop) {},
});
```
