# Чем setTimeout отличается от setImmediate

> [!NOTE]
> `setTimeout()` планирует callback после минимальной задержки в фазе timers, а `setImmediate()` планирует callback в фазе check текущего или следующего цикла event loop.

## Главное

```js
setTimeout(() => {
  console.log("timeout");
}, 0);

setImmediate(() => {
  console.log("immediate");
});
```

Порядок между ними не всегда стоит считать надежным, если они запланированы из главного модуля.

## setTimeout

```js
setTimeout(callback, delay);
```

`delay` - минимальная задержка, а не точное время выполнения. Если event loop занят, callback выполнится позже.

## setImmediate

```js
setImmediate(callback);
```

`setImmediate` выполняется в check-фазе, после poll-фазы.

## Внутри I/O callback

Внутри I/O callback `setImmediate` часто выполняется раньше `setTimeout(..., 0)`.

```js
import { readFile } from "node:fs";

readFile("file.txt", () => {
  setTimeout(() => console.log("timeout"), 0);
  setImmediate(() => console.log("immediate"));
});
```

## Что выбрать

- Нужна задержка по времени: `setTimeout`.
- Нужно выполнить callback после текущего I/O turn: `setImmediate`.
- Нужна promise-микрозадача: `queueMicrotask` или `Promise.resolve().then(...)`.

## Мини-шпаргалка

- `setTimeout` работает через timers.
- `setImmediate` работает через check phase.
- `delay` у timeout - минимальная задержка.
- Порядок может зависеть от контекста.
- В I/O callback `setImmediate` обычно предсказуемее для "после I/O".
