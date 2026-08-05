# Что делает “debounce”?

> [!NOTE]
> Debounce откладывает вызов функции до тех пор, пока события не прекратятся на заданное время.

## Вопрос

Что такое debounce и где его применяют?

## Определение

Debounce ограничивает частые вызовы функции. Каждый новый вызов сбрасывает таймер. Функция выполнится только после паузы длиной `delay`.

Это полезно для поиска по вводу, автосохранения и resize-событий.

## Пример реализации

```javascript
function debounce(fn, delay) {
  let timeoutId;

  return function (...args) {
    clearTimeout(timeoutId);

    timeoutId = setTimeout(() => {
      fn.apply(this, args);
    }, delay);
  };
}
```

## Использование

```javascript
const search = debounce((query) => {
  fetch(`/api/search?q=${query}`);
}, 300);

input.addEventListener('input', (event) => {
  search(event.target.value);
});
```

Запрос отправится только когда пользователь перестанет печатать на 300 мс.

## Debounce vs обычный вызов

```text
input: a b c d
without debounce -> 4 calls
with debounce -> 1 call after pause
```

## Когда использовать

- поиск по input;
- автосохранение;
- проверка валидности;
- resize после окончания изменения размера;
- дорогие вычисления после серии событий.

## Мини-шпаргалка

```javascript
const debounced = debounce(callback, 300);
```
