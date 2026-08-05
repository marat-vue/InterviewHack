# Что такое Canvas API?

> [!NOTE]
> Canvas API позволяет рисовать 2D-графику пиксельно через JavaScript внутри элемента `<canvas>`.

## Вопрос

Для чего нужен Canvas API?

## Определение

`<canvas>` - HTML-элемент для рисования. Сам по себе он только создает область. Рисование выполняется через JavaScript-контекст, чаще всего `2d`.

Canvas подходит для графиков, игр, визуализаций, редакторов изображений и динамической графики.

## Базовый пример

```html
<canvas id="canvas" width="300" height="150"></canvas>
```

```javascript
const canvas = document.querySelector('#canvas');
const ctx = canvas.getContext('2d');

ctx.fillStyle = 'tomato';
ctx.fillRect(20, 20, 120, 80);
```

`fillRect(x, y, width, height)` рисует заполненный прямоугольник.

## Рисование текста

```javascript
ctx.font = '24px sans-serif';
ctx.fillStyle = 'black';
ctx.fillText('Hello', 20, 130);
```

## Очистка canvas

```javascript
ctx.clearRect(0, 0, canvas.width, canvas.height);
```

Canvas не хранит отдельные DOM-элементы для фигур. Если нужно изменить сцену, обычно очищают область и рисуют заново.

## Canvas vs SVG

| Canvas | SVG |
| --- | --- |
| пиксельное рисование | векторные элементы |
| хорошо для частого перерисовывания | хорошо для схем и иконок |
| фигуры не являются DOM-узлами | элементы доступны в DOM |
| удобно для игр и графики | удобно для интерактивных диаграмм |

## Мини-шпаргалка

```javascript
const ctx = canvas.getContext('2d');

ctx.fillRect(x, y, width, height);
ctx.clearRect(0, 0, canvas.width, canvas.height);
ctx.drawImage(image, x, y);
```
