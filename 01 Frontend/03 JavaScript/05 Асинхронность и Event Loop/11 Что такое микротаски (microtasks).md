# Что такое микротаски (microtasks)?

> [!NOTE] Коротко
> Микротаски выполняются сразу после текущего синхронного кода и перед следующей макротаской.

## Вопрос

Что такое microtasks и почему они выполняются раньше `setTimeout`?

## Определение

Микротаски - задачи с высоким приоритетом в Event Loop. Они используются для продолжений промисов и некоторых внутренних реакций платформы.

Когда Call Stack становится пустым, JavaScript сначала выполняет все микротаски. Только после этого Event Loop переходит к следующей макротаске.

## Что создает микротаски

- `Promise.then`;
- `Promise.catch`;
- `Promise.finally`;
- `queueMicrotask`;
- `MutationObserver`;
- в Node.js также есть `process.nextTick`, но у него особый приоритет.

## Пример порядка

```javascript
console.log(1);

setTimeout(() => console.log(2), 0);

Promise.resolve().then(() => console.log(3));

console.log(4);

// 1
// 4
// 3
// 2
```

Промисовая микротаска выполняется перед таймером.

## Важный нюанс

Очередь микротасок очищается полностью. Если микротаска добавляет новую микротаску, новая тоже выполнится до перехода к макротаскам.

```javascript
queueMicrotask(() => {
  console.log('first');

  queueMicrotask(() => {
    console.log('second');
  });
});
```

Если бесконечно добавлять микротаски, можно заблокировать переход к таймерам и рендеру.

## Мини-шпаргалка

```javascript
Promise.resolve().then(fn); // microtask
queueMicrotask(fn);         // microtask
setTimeout(fn, 0);          // macrotask
```
