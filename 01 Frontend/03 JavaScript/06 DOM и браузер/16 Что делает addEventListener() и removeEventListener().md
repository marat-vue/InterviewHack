# Что делает addEventListener() и removeEventListener()?

> [!NOTE] Коротко
> `addEventListener()` добавляет обработчик события, а `removeEventListener()` удаляет ранее добавленный обработчик.

## Вопрос

Как правильно подписываться на DOM-события и отписываться от них?

## addEventListener()

`addEventListener(type, listener, options)` вешает функцию-обработчик на элемент.

```javascript
const button = document.querySelector('button');

function handleClick(event) {
  console.log('clicked', event.target);
}

button.addEventListener('click', handleClick);
```

На одно событие можно добавить несколько обработчиков.

## removeEventListener()

Чтобы удалить обработчик, нужно передать ту же самую функцию.

```javascript
button.removeEventListener('click', handleClick);
```

Если передать другую функцию, обработчик не удалится.

## Важный пример с ошибкой

```javascript
button.addEventListener('click', () => {
  console.log('clicked');
});

button.removeEventListener('click', () => {
  console.log('clicked');
});
```

Эти две стрелочные функции выглядят одинаково, но это разные объекты функций. Удаление не сработает.

## Опции

```javascript
button.addEventListener('click', handleClick, {
  once: true,
  passive: true,
  capture: false,
});
```

| Опция | Что делает |
| --- | --- |
| `once` | удалить обработчик после первого вызова |
| `passive` | обработчик не будет вызывать `preventDefault()` |
| `capture` | слушать событие на фазе погружения |

## Мини-шпаргалка

```javascript
element.addEventListener('click', handler);
element.removeEventListener('click', handler);
```
