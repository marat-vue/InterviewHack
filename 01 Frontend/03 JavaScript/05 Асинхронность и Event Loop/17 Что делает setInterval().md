# Что делает setInterval()?

> [!NOTE] Коротко
> `setInterval()` запускает callback повторно через заданные интервалы и возвращает идентификатор для отмены.

## Вопрос

Чем `setInterval()` отличается от `setTimeout()`?

## Определение

`setInterval(callback, delay)` планирует повторяющийся запуск callback-функции. Среда выполнения будет пытаться вызывать callback каждые `delay` миллисекунд, пока интервал не отменят через `clearInterval()`.

## Пример

```javascript
const intervalId = setInterval(() => {
  console.log('tick');
}, 1000);
```

Каждую секунду будет выводиться `tick`.

## Отмена интервала

```javascript
let count = 0;

const id = setInterval(() => {
  count++;
  console.log(count);

  if (count === 3) {
    clearInterval(id);
  }
}, 1000);
```

После третьего срабатывания интервал остановится.

## Важный нюанс

Если callback выполняется долго, вызовы могут задерживаться. `setInterval` не гарантирует идеальную точность.

```javascript
setInterval(() => {
  const start = Date.now();

  while (Date.now() - start < 1500) {}

  console.log('done');
}, 1000);
```

Callback занимает больше времени, чем интервал, поэтому расписание начнет отставать.

## Альтернатива через рекурсивный setTimeout

```javascript
function tick() {
  console.log('tick');

  setTimeout(tick, 1000);
}

setTimeout(tick, 1000);
```

Так следующий запуск планируется после завершения текущего.

## Мини-шпаргалка

```javascript
const id = setInterval(callback, delay);
clearInterval(id);
```
