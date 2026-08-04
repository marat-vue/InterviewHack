# Что делает Web Worker?

> [!NOTE] Коротко
> Web Worker запускает JavaScript-код в отдельном потоке, чтобы тяжелые вычисления не блокировали интерфейс.

## Вопрос

Зачем нужен Web Worker и чем он отличается от обычного асинхронного кода?

## Определение

Web Worker - браузерный API для выполнения JavaScript в фоновом потоке. Основной поток отвечает за UI и DOM, а worker может заниматься тяжелыми вычислениями.

Worker не имеет доступа к DOM напрямую. Обмен данными происходит через сообщения.

## Создание worker

```javascript
const worker = new Worker('worker.js');

worker.postMessage({
  type: 'CALCULATE',
  payload: [1, 2, 3],
});
```

## Получение ответа

```javascript
worker.addEventListener('message', (event) => {
  console.log(event.data);
});
```

## Код внутри worker.js

```javascript
self.addEventListener('message', (event) => {
  const numbers = event.data.payload;
  const sum = numbers.reduce((total, number) => total + number, 0);

  self.postMessage({ type: 'RESULT', payload: sum });
});
```

## Когда использовать

- сложные вычисления;
- обработка больших массивов;
- парсинг больших файлов;
- работа с изображениями;
- задачи, которые могут подвесить интерфейс.

## Когда не нужен

Для обычного `fetch`, небольших вычислений и простой UI-логики worker чаще всего избыточен.

## Мини-шпаргалка

```javascript
const worker = new Worker('worker.js');
worker.postMessage(data);
worker.onmessage = (event) => console.log(event.data);
worker.terminate();
```
