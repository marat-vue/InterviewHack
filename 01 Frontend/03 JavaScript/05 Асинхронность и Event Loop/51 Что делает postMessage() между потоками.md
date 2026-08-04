# Что делает postMessage() между потоками?

> [!NOTE] Коротко
> `postMessage()` отправляет данные между основным потоком и worker-потоком.

## Вопрос

Как основной поток и Web Worker обмениваются данными?

## Определение

`postMessage()` - метод для асинхронной отправки сообщений между разными контекстами выполнения. В случае Web Worker основной поток отправляет сообщение worker-у, а worker отвечает обратно тоже через `postMessage()`.

Получатель слушает событие `message`.

## Основной поток

```javascript
const worker = new Worker('worker.js');

worker.postMessage({ numbers: [1, 2, 3] });

worker.addEventListener('message', (event) => {
  console.log(event.data); // { sum: 6 }
});
```

## worker.js

```javascript
self.addEventListener('message', (event) => {
  const numbers = event.data.numbers;
  const sum = numbers.reduce((total, number) => total + number, 0);

  self.postMessage({ sum });
});
```

## Что можно передавать

Данные передаются через structured clone algorithm. Можно отправлять объекты, массивы, строки, числа, `Map`, `Set`, `ArrayBuffer` и другие структурируемые значения.

Функции и DOM-элементы передавать нельзя.

## Transferable objects

Для больших бинарных данных можно передать владение объектом, например `ArrayBuffer`.

```javascript
const buffer = new ArrayBuffer(1024);

worker.postMessage(buffer, [buffer]);
```

После передачи основной поток больше не владеет этим буфером.

## Мини-шпаргалка

```javascript
worker.postMessage(data);

worker.onmessage = (event) => {
  console.log(event.data);
};
```
