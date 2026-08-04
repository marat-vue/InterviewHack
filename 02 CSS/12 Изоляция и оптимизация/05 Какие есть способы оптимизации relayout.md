# Какие есть способы оптимизации relayout?

> [!NOTE]
> Оптимизация relayout сводится к тому, чтобы реже менять геометрию страницы, ограничивать область изменений, избегать layout thrashing и использовать для анимаций свойства, которые не требуют пересчета layout.

## Главное

Relayout становится проблемой, когда изменения часто повторяются или затрагивают большую часть страницы.

```text
many layout changes
  -> more CPU work
  -> lower FPS
  -> worse interaction latency
```

## Анимировать transform вместо размеров и координат

```css
/* хуже для движения */
.panel {
  left: -320px;
}

/* лучше для движения */
.panel {
  transform: translateX(-100%);
}
```

`transform` обычно не требует пересчета layout.

## Избегать layout thrashing

Плохо чередовать чтение layout и запись стилей в цикле.

```js
items.forEach((item) => {
  const height = item.offsetHeight;
  item.style.height = `${height + 10}px`;
});
```

Лучше сначала собрать измерения, потом применить изменения.

```js
const heights = items.map((item) => item.offsetHeight);

items.forEach((item, index) => {
  item.style.height = `${heights[index] + 10}px`;
});
```

## Ограничивать область изменений

CSS containment помогает подсказать браузеру, что изменения внутри блока не должны влиять на внешнюю страницу.

```css
.widget {
  contain: layout paint;
}
```

Использовать `contain` нужно осознанно: оно меняет некоторые правила layout и paint.

## Батчить DOM-изменения

Частые маленькие изменения лучше группировать.

```js
requestAnimationFrame(() => {
  element.classList.add("is-open");
});
```

Так браузеру проще выполнить работу в правильный кадр.

## Мини-шпаргалка

- Не анимируй `width`, `height`, `top`, `left`, если можно `transform`.
- Не чередуй чтение layout и запись стилей в цикле.
- Группируй DOM-изменения.
- Ограничивай область влияния через архитектуру и иногда `contain`.
- Большие списки лучше виртуализировать.
- Проверяй Performance panel, а не оптимизируй наугад.
