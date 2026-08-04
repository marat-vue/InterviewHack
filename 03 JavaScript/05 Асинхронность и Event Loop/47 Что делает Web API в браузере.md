# Что делает Web API в браузере?

> [!NOTE] Коротко
> Web API - возможности браузера, которые доступны JavaScript-коду, но выполняются средой браузера, а не самим JS-языком.

## Вопрос

Что такое Web API и как они связаны с асинхронностью?

## Определение

Web API - набор браузерных интерфейсов: DOM, таймеры, `fetch`, события, WebSocket, Storage, Canvas и многие другие.

JavaScript вызывает эти API, а браузер выполняет соответствующую работу. Когда результат готов, callback или продолжение промиса возвращается в JavaScript через Event Loop.

## Примеры Web API

```javascript
setTimeout(() => console.log('timer'), 1000);

fetch('/api/data').then((response) => response.json());

button.addEventListener('click', () => {
  console.log('clicked');
});
```

`setTimeout`, `fetch` и `addEventListener` - не часть ядра языка JavaScript, а возможности браузерной среды.

## Как это работает с Event Loop

1. JS вызывает Web API.
2. Браузер берет работу на себя.
3. JS продолжает выполнять следующий код.
4. Когда результат готов, обработчик попадает в очередь.
5. Event Loop выполнит его, когда Call Stack будет свободен.

## Web API vs ECMAScript

| Что | Пример |
| --- | --- |
| ECMAScript | `Array`, `Promise`, `Map`, функции, объекты |
| Web API | DOM, `fetch`, `setTimeout`, WebSocket |

`Promise` является частью языка, а `fetch` - частью Web API.

## Мини-шпаргалка

```text
JavaScript calls Web API -> browser does work -> callback/promise continuation returns through Event Loop
```
