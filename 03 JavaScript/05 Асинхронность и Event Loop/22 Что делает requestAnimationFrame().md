# Что делает requestAnimationFrame()?

> [!NOTE] Коротко
> `requestAnimationFrame()` планирует callback перед следующей перерисовкой браузера и подходит для анимаций.

## Вопрос

Почему для анимаций лучше использовать `requestAnimationFrame()`, а не `setInterval()`?

## Определение

`requestAnimationFrame(callback)` просит браузер вызвать callback перед следующим кадром отрисовки. Браузер сам выбирает подходящий момент, синхронизированный с частотой экрана.

Метод возвращает id, который можно передать в `cancelAnimationFrame()`.

## Пример

```javascript
let x = 0;

function animate() {
  x += 2;
  element.style.transform = `translateX(${x}px)`;

  requestAnimationFrame(animate);
}

requestAnimationFrame(animate);
```

Callback вызывается перед каждым новым кадром.

## Аргумент timestamp

```javascript
function step(timestamp) {
  console.log(timestamp);

  requestAnimationFrame(step);
}

requestAnimationFrame(step);
```

`timestamp` - время текущего кадра. Его используют, чтобы считать движение по времени, а не по количеству кадров.

## Отмена

```javascript
const id = requestAnimationFrame(() => {
  console.log('frame');
});

cancelAnimationFrame(id);
```

## Отличие от таймеров

| Метод | Для чего |
| --- | --- |
| `setTimeout` | выполнить позже |
| `setInterval` | повторять по времени |
| `requestAnimationFrame` | обновлять UI перед кадром |

## Мини-шпаргалка

```javascript
const id = requestAnimationFrame(callback);
cancelAnimationFrame(id);
```
