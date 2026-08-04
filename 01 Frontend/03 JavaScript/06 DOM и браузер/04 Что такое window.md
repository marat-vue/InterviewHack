# Что такое window?

> [!NOTE] Коротко
> `window` - глобальный объект браузера, который представляет окно или вкладку и хранит браузерные API.

## Вопрос

Что такое `window` в JavaScript?

## Определение

`window` - главный глобальный объект в браузере. В нем находятся глобальные переменные, функции и многие Web API: `document`, `location`, `history`, `navigator`, таймеры и события окна.

Когда вы объявляете глобальную переменную через `var`, она становится свойством `window`.

## Примеры

```javascript
console.log(window.document);
console.log(window.location.href);
console.log(window.innerWidth);
```

Многие свойства можно писать без `window.`:

```javascript
setTimeout(() => console.log('timer'), 1000);

// то же самое:
window.setTimeout(() => console.log('timer'), 1000);
```

## События window

```javascript
window.addEventListener('resize', () => {
  console.log(window.innerWidth);
});
```

`window` используют для событий уровня вкладки: resize, scroll, load, beforeunload.

## Что хранится в window

| Свойство | Значение |
| --- | --- |
| `document` | DOM текущей страницы |
| `location` | текущий URL |
| `history` | история навигации |
| `navigator` | информация о браузере |
| `localStorage` | локальное хранилище |

## Мини-шпаргалка

```javascript
window.document;
window.location.href;
window.addEventListener('resize', handler);
```
