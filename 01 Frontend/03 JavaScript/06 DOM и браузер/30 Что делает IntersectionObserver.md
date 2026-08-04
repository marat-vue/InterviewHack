# Что делает IntersectionObserver?

> [!NOTE] Коротко
> `IntersectionObserver` асинхронно отслеживает, пересекается ли элемент с viewport или другим контейнером.

## Вопрос

Зачем нужен `IntersectionObserver`?

## Определение

`IntersectionObserver` - браузерный API для наблюдения за видимостью элемента. Он сообщает, когда элемент появляется в области просмотра или выходит из нее.

Это лучше, чем постоянно слушать `scroll` и вручную считать координаты.

## Пример

```javascript
const target = document.querySelector('.section');

const observer = new IntersectionObserver((entries) => {
  entries.forEach((entry) => {
    if (entry.isIntersecting) {
      console.log('Element is visible');
    }
  });
});

observer.observe(target);
```

## entry

```javascript
console.log(entry.target);
console.log(entry.isIntersecting);
console.log(entry.intersectionRatio);
```

`entry` описывает состояние пересечения конкретного элемента.

## Опции

```javascript
const observer = new IntersectionObserver(callback, {
  root: null,
  rootMargin: '0px',
  threshold: 0.5,
});
```

| Опция | Значение |
| --- | --- |
| `root` | контейнер наблюдения, `null` означает viewport |
| `rootMargin` | отступы вокруг root |
| `threshold` | доля видимости для срабатывания |

## Где используется

- lazy loading изображений;
- бесконечная прокрутка;
- запуск анимации при появлении;
- аналитика видимости блоков.

## Мини-шпаргалка

```javascript
const observer = new IntersectionObserver(callback, options);
observer.observe(element);
observer.unobserve(element);
observer.disconnect();
```
