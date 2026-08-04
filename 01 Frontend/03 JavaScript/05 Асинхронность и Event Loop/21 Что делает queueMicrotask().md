# Что делает queueMicrotask()?

> [!NOTE] Коротко
> `queueMicrotask()` ставит callback в очередь микротасок, чтобы он выполнился после текущего синхронного кода и перед макротасками.

## Вопрос

Когда использовать `queueMicrotask()` и чем он похож на `Promise.resolve().then()`?

## Определение

`queueMicrotask(callback)` явно добавляет функцию в Microtask Queue. Callback выполнится, когда текущий Call Stack освободится, но до следующей макротаски вроде `setTimeout`.

## Пример

```javascript
console.log('A');

queueMicrotask(() => {
  console.log('B');
});

console.log('C');

// A
// C
// B
```

Микротаска выполняется после синхронного кода.

## Сравнение с Promise.then

```javascript
queueMicrotask(fn);

Promise.resolve().then(fn);
```

Оба варианта планируют микротаску. `queueMicrotask()` показывает намерение напрямую: "поставить задачу в очередь микротасок".

## Порядок с таймером

```javascript
setTimeout(() => console.log('timeout'), 0);

queueMicrotask(() => console.log('microtask'));

console.log('sync');

// sync
// microtask
// timeout
```

## Осторожно с бесконечной очередью

```javascript
function loop() {
  queueMicrotask(loop);
}

loop();
```

Такая цепочка может не дать Event Loop перейти к таймерам, событиям и рендеру.

## Мини-шпаргалка

```javascript
queueMicrotask(callback); // microtask
setTimeout(callback, 0);  // macrotask
```
