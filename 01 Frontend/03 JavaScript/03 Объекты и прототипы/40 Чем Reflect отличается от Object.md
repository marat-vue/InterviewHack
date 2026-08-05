# `Reflect` vs `Object`

> [!NOTE]
> `Object` - набор исторических утилит для работы с объектами. `Reflect` - API для метапрограммирования, близкий к внутренним операциям JavaScript и удобный вместе с `Proxy`.

## Вопрос

Чем `Reflect` отличается от `Object`?

## Главное различие

`Object` чаще используют для обычных задач:

```javascript
Object.keys(obj);
Object.assign({}, obj);
Object.create(proto);
```

`Reflect` чаще используют для низкоуровневых операций:

```javascript
Reflect.get(obj, "name");
Reflect.set(obj, "name", "Anna");
Reflect.has(obj, "name");
```

## Возвращаемые значения

Некоторые методы `Object` бросают ошибку при неуспехе, а `Reflect` возвращает boolean.

```javascript
const obj = Object.freeze({});

Reflect.defineProperty(obj, "x", { value: 1 }); // false
```

`Object.defineProperty` в похожей ситуации может выбросить исключение.

## Операторы как методы

`Reflect` превращает операции языка в функции.

```javascript
"name" in obj;
Reflect.has(obj, "name");
```

```javascript
delete obj.name;
Reflect.deleteProperty(obj, "name");
```

Это удобно, когда операцию нужно передавать, оборачивать или использовать внутри Proxy.

## Связь с Proxy

Методы `Reflect` часто совпадают по имени с traps.

```javascript
const proxy = new Proxy(target, {
  get(target, prop, receiver) {
    return Reflect.get(target, prop, receiver);
  },
});
```

Это делает код ловушек понятным: trap перехватывает операцию, `Reflect` выполняет стандартное поведение.

## Что есть только у `Object`

Не все методы `Object` имеют смысл в `Reflect`.

```javascript
Object.keys(obj);
Object.values(obj);
Object.entries(obj);
Object.freeze(obj);
```

`Reflect` не заменяет `Object` полностью.

## Мини-шпаргалка

| Задача | Обычно |
| --- | --- |
| получить ключи | `Object.keys` |
| скопировать объект | `Object.assign` или spread |
| создать с прототипом | `Object.create` |
| прочитать свойство мета-способом | `Reflect.get` |
| записать свойство мета-способом | `Reflect.set` |
| стандартное поведение в Proxy | `Reflect.*` |
