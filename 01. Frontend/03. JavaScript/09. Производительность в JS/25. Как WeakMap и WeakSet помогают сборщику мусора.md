# Как WeakMap и WeakSet помогают сборщику мусора?

> [!NOTE]
> `WeakMap` и `WeakSet` хранят слабые ссылки на объекты, поэтому не мешают сборщику мусора удалять эти объекты.

## Вопрос

Почему `WeakMap` и `WeakSet` полезны для памяти?

## Проблема обычных Map и Set

```javascript
const map = new Map();

let element = document.querySelector('.button');

map.set(element, { clicked: true });
element = null;
```

Если DOM-элемент остался ключом в `Map`, он все еще достижим через `map` и не может быть собран GC.

## WeakMap

```javascript
const weakMap = new WeakMap();

let element = document.querySelector('.button');

weakMap.set(element, { clicked: true });
element = null;
```

Если на элемент больше нет сильных ссылок, запись в `WeakMap` не удерживает его в памяти.

## WeakSet

```javascript
const processed = new WeakSet();

function markProcessed(object) {
  processed.add(object);
}
```

`WeakSet` удобен для отметки объектов без продления их жизни.

## Почему их нельзя перебрать

У `WeakMap` и `WeakSet` нет `size`, `keys()`, `values()` и обычного перебора. Состав коллекции зависит от работы GC, а она недетерминирована.

## Когда использовать

- метаданные DOM-элементов;
- кэш для объектов;
- отметка обработанных объектов;
- приватные данные, привязанные к объектам.

## Мини-шпаргалка

```javascript
const weakMap = new WeakMap();
weakMap.set(objectKey, value);
weakMap.get(objectKey);

const weakSet = new WeakSet();
weakSet.add(object);
```
