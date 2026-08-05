# Как удалить элемент из DOM?

> [!NOTE]
> DOM-элемент можно удалить методом `element.remove()` или через родителя методом `removeChild()`.

## Вопрос

Как удалить элемент со страницы через JavaScript?

## remove()

Самый простой способ - вызвать `remove()` у элемента.

```javascript
const message = document.querySelector('.message');

message.remove();
```

Элемент исчезнет из DOM.

## Проверка на null

```javascript
const message = document.querySelector('.message');

if (message) {
  message.remove();
}
```

`querySelector()` может вернуть `null`, если элемент не найден.

## removeChild()

Старый способ - удалить элемент через родителя.

```javascript
const list = document.querySelector('.list');
const item = list.querySelector('.item');

list.removeChild(item);
```

Сейчас чаще используют `remove()`, потому что он короче.

## Очистка содержимого

```javascript
const list = document.querySelector('.list');

list.replaceChildren();
```

`replaceChildren()` без аргументов удаляет всех дочерних узлов.

## Мини-шпаргалка

```javascript
element.remove();
parent.removeChild(child);
parent.replaceChildren();
```
