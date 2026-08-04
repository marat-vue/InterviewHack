# Чем DOMContentLoaded отличается от load?

> [!NOTE] Коротко
> `DOMContentLoaded` срабатывает, когда построен DOM, а `load` - когда загрузились еще и внешние ресурсы страницы.

## Вопрос

Когда использовать `DOMContentLoaded`, а когда `load`?

## DOMContentLoaded

`DOMContentLoaded` срабатывает, когда браузер разобрал HTML и построил DOM-дерево. Картинки, шрифты и другие ресурсы могут еще загружаться.

```javascript
document.addEventListener('DOMContentLoaded', () => {
  console.log('DOM is ready');
});
```

Это событие удобно для инициализации DOM-логики.

## load

`load` срабатывает позже: когда загрузилась вся страница вместе с зависимыми ресурсами.

```javascript
window.addEventListener('load', () => {
  console.log('Page and resources are loaded');
});
```

Его используют, когда нужны размеры изображений, готовые внешние ресурсы или полная загрузка страницы.

## Сравнение

| Событие | Когда срабатывает | Где слушать |
| --- | --- | --- |
| `DOMContentLoaded` | DOM построен | `document` |
| `load` | DOM и ресурсы загружены | `window` |

## Пример порядка

```javascript
document.addEventListener('DOMContentLoaded', () => {
  console.log('DOMContentLoaded');
});

window.addEventListener('load', () => {
  console.log('load');
});
```

Обычно сначала будет `DOMContentLoaded`, потом `load`.

## Мини-шпаргалка

```javascript
document.addEventListener('DOMContentLoaded', initDom);
window.addEventListener('load', initAfterResources);
```
