# Что делает AbortController и AbortSignal?

> [!NOTE]
> `AbortController` создает сигнал отмены, а `AbortSignal` передается в асинхронную операцию, чтобы ее можно было прервать.

## Вопрос

Как отменять `fetch` и другие асинхронные операции через `AbortController`?

## Определение

`AbortController` - объект управления отменой. У него есть свойство `signal` и метод `abort()`.

`AbortSignal` - объект-сигнал, который передается операции. Когда вызывают `controller.abort()`, сигнал переходит в состояние отмены, а операция может завершиться с ошибкой `AbortError`.

## Пример с fetch

```javascript
const controller = new AbortController();

async function loadData() {
  try {
    const response = await fetch('/api/data', {
      signal: controller.signal,
    });

    return await response.json();
  } catch (error) {
    if (error.name === 'AbortError') {
      console.log('Request canceled');
      return;
    }

    throw error;
  }
}

controller.abort();
```

## Проверка сигнала

```javascript
console.log(controller.signal.aborted); // false

controller.abort();

console.log(controller.signal.aborted); // true
```

## Где применяется

- отмена `fetch`;
- отмена stream-операций;
- отмена долгих пользовательских задач;
- таймауты запросов;
- очистка эффектов в UI-фреймворках.

## Мини-шпаргалка

```javascript
const controller = new AbortController();

fetch(url, { signal: controller.signal });
controller.abort();
```
