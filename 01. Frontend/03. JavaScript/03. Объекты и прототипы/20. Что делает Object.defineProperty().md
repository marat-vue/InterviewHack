# `Object.defineProperty()`

> [!NOTE]
> `Object.defineProperty()` добавляет или переопределяет свойство объекта через дескриптор: можно настроить значение, запись, перечисление, удаление, getter и setter.

## Вопрос

Что делает `Object.defineProperty()`?

## Синтаксис

```javascript
Object.defineProperty(obj, propertyName, descriptor);
```

Пример:

```javascript
const user = {};

Object.defineProperty(user, "id", {
  value: 1,
  writable: false,
  enumerable: true,
  configurable: false,
});
```

## Дескриптор свойства

Дескриптор описывает, как работает свойство.

Для data property:

```javascript
{
  value: 1,
  writable: true,
  enumerable: true,
  configurable: true
}
```

Значения по умолчанию при `defineProperty` - `false` для флагов.

```javascript
Object.defineProperty(obj, "x", {
  value: 1,
});
```

`x` будет `writable: false`, `enumerable: false`, `configurable: false`.

## Флаги

| Флаг | Что означает |
| --- | --- |
| `value` | значение свойства |
| `writable` | можно ли менять значение |
| `enumerable` | видно ли в `Object.keys`/`for...in` |
| `configurable` | можно ли удалить/переопределить дескриптор |

## Getter/setter descriptor

Вместо `value/writable` можно использовать `get/set`.

```javascript
const user = {
  firstName: "Anna",
  lastName: "Smith",
};

Object.defineProperty(user, "fullName", {
  get() {
    return `${this.firstName} ${this.lastName}`;
  },
  set(value) {
    [this.firstName, this.lastName] = value.split(" ");
  },
  enumerable: true,
});
```

Нельзя одновременно использовать `value` и `get`.

## Неперечисляемое свойство

```javascript
const user = { name: "Anna" };

Object.defineProperty(user, "password", {
  value: "secret",
  enumerable: false,
});

Object.keys(user); // ["name"]
```

## Мини-шпаргалка

```javascript
Object.defineProperty(obj, "key", {
  value: "value",
  writable: false,
  enumerable: true,
  configurable: false,
});
```

| Нужно | Настройка |
| --- | --- |
| readonly | `writable: false` |
| скрыть из `Object.keys` | `enumerable: false` |
| запретить delete | `configurable: false` |
| вычисляемое свойство | `get()` |
| контроль записи | `set(value)` |
