# Чем window отличается от document?

> [!NOTE] Коротко
> `window` представляет вкладку браузера целиком, а `document` представляет DOM текущей страницы.

## Вопрос

В чем разница между `window` и `document`?

## Определение

`window` - глобальный объект браузерного окружения. Он хранит API вкладки: адрес, историю, размеры окна, таймеры, события, хранилища.

`document` - объект внутри `window`, который отвечает за HTML-документ и DOM-дерево.

## Пример связи

```javascript
console.log(window.document === document); // true
```

`document` доступен напрямую, потому что он является свойством `window`.

## Что где искать

```javascript
window.innerWidth;       // ширина окна
window.location.href;    // текущий URL
document.body;           // body страницы
document.querySelector('h1'); // поиск элемента
```

## Сравнение

| `window` | `document` |
| --- | --- |
| вкладка или окно браузера | HTML-документ |
| содержит браузерные API | содержит DOM |
| работает с URL, историей, размерами | работает с элементами страницы |
| родительский объект | свойство внутри `window` |

## Частая ошибка

```javascript
window.querySelector('h1'); // TypeError
```

Селекторы DOM находятся у `document`, а не у `window`.

## Мини-шпаргалка

```javascript
window.document; // document лежит внутри window
document.body;   // DOM страницы
window.history;  // история вкладки
```
