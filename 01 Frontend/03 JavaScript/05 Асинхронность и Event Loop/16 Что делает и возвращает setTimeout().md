# Что делает и возвращает setTimeout()?

> [!NOTE]
> `setTimeout()` планирует одноразовый запуск callback-функции после минимальной задержки и возвращает идентификатор таймера.

## Вопрос

Что делает `setTimeout()` и что он возвращает?

## Определение

`setTimeout(callback, delay)` ставит callback в расписание. Когда пройдет минимум `delay` миллисекунд, среда выполнения сможет добавить callback в очередь задач.

Важно: задержка не является точной гарантией времени выполнения. Callback запустится только тогда, когда Call Stack будет свободен и до него дойдет Event Loop.

## Пример

```javascript
const timerId = setTimeout(() => {
  console.log('done');
}, 1000);

console.log(timerId);
```

В браузере обычно возвращается числовой id. В Node.js возвращается объект таймера.

## Отмена таймера

```javascript
const id = setTimeout(() => {
  console.log('will not run');
}, 1000);

clearTimeout(id);
```

Если вызвать `clearTimeout()` до выполнения callback, таймер будет отменен.

## setTimeout с задержкой 0

```javascript
console.log('start');

setTimeout(() => console.log('timeout'), 0);

console.log('end');

// start
// end
// timeout
```

`0` означает "как можно скорее после текущего синхронного кода", а не "немедленно".

## Мини-шпаргалка

```javascript
const id = setTimeout(callback, delay);
clearTimeout(id);
```
