# `Proxy`

> [!NOTE]
> `Proxy` создает обертку над объектом или функцией и позволяет перехватывать операции: чтение, запись, удаление, проверку `in`, вызов функции, `new` и другие.

## Вопрос

Что делает объект `Proxy`?

## Синтаксис

```javascript
const proxy = new Proxy(target, handler);
```

- `target` - исходный объект или функция;
- `handler` - объект с ловушками (traps).

## Перехват чтения `get`

```javascript
const user = {
  name: "Anna",
};

const proxy = new Proxy(user, {
  get(target, prop) {
    if (prop in target) {
      return target[prop];
    }

    return "Нет такого свойства";
  },
});

proxy.name; // "Anna"
proxy.age;  // "Нет такого свойства"
```

## Перехват записи `set`

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

Trap `set` должен вернуть boolean.

## Перехват `in`

```javascript
const user = { name: "Anna", password: "secret" };

const proxy = new Proxy(user, {
  has(target, prop) {
    if (prop === "password") return false;

    return prop in target;
  },
});

"password" in proxy; // false
```

## Перехват удаления

```javascript
const proxy = new Proxy(user, {
  deleteProperty(target, prop) {
    if (prop === "id") return false;

    delete target[prop];
    return true;
  },
});
```

## Где используется

`Proxy` полезен для:

- валидации данных;
- логирования доступа;
- реактивности;
- виртуальных свойств;
- защиты объектов;
- метапрограммирования.

Например, Vue 3 использует `Proxy` как основу системы реактивности.

## Подводные камни

- Proxy может усложнить отладку;
- не все операции легко прозрачно проксировать;
- есть ограничения-инварианты языка;
- частые traps могут влиять на производительность.

## Мини-шпаргалка

| Trap | Что перехватывает |
| --- | --- |
| `get` | чтение `obj.prop` |
| `set` | запись `obj.prop = value` |
| `has` | оператор `in` |
| `deleteProperty` | `delete obj.prop` |
| `ownKeys` | перечисление ключей |
| `apply` | вызов функции |
| `construct` | вызов через `new` |
