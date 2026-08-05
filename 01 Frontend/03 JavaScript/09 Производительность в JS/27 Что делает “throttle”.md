# Что делает “throttle”?

> [!NOTE]
> Throttle ограничивает частоту вызова функции: не чаще одного раза за заданный интервал.

## Вопрос

Что такое throttle и чем он отличается от debounce?

## Определение

Throttle пропускает вызовы функции с заданной частотой. Если событие происходит слишком часто, функция все равно выполняется максимум один раз за `delay`.

Это удобно для scroll, mousemove, resize и других потоковых событий.

## Пример реализации

```javascript
function throttle(fn, delay) {
  let lastCall = 0;

  return function (...args) {
    const now = Date.now();

    if (now - lastCall >= delay) {
      lastCall = now;
      fn.apply(this, args);
    }
  };
}
```

## Использование

```javascript
const onScroll = throttle(() => {
  console.log(window.scrollY);
}, 200);

window.addEventListener('scroll', onScroll);
```

При частом scroll обработчик будет выполняться не чаще одного раза в 200 мс.

## Debounce vs throttle

| Прием | Как работает | Пример |
| --- | --- | --- |
| Debounce | ждет паузу после серии событий | поиск по input |
| Throttle | выполняет не чаще заданного интервала | scroll progress |

## Когда использовать

- scroll-позиция;
- resize во время изменения размера;
- drag/mousemove;
- обновление прогресс-бара;
- ограничение дорогого обработчика.

## Мини-шпаргалка

```javascript
const throttled = throttle(callback, 200);
```
