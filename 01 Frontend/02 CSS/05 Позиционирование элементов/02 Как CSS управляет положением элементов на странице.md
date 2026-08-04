# Как CSS управляет положением элементов на странице?

> [!NOTE]
> CSS управляет положением элементов через нормальный поток документа, Box Model, `display`, Flexbox, Grid, `position`, transform и отступы.

## Главное

Расположение элемента определяется не одним свойством, а комбинацией механизмов.

```text
HTML order
  -> normal flow
  -> display/layout mode
  -> box model
  -> position/offset
  -> transform
```

## Normal flow

Без специальных layout-правил блочные элементы идут сверху вниз, а inline-элементы располагаются внутри строк.

```html
<h1>Заголовок</h1>
<p>Абзац текста</p>
```

## Display

```css
.toolbar {
  display: flex;
  gap: 8px;
}

.gallery {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
```

`display` может включить Flexbox или Grid для управления дочерними элементами.

## Position

```css
.tooltip {
  position: absolute;
  top: 100%;
  left: 0;
}
```

`position` используется для точных смещений, фиксированных элементов, подсказок, бейджей и модальных окон.

## Transform

```css
.card:hover {
  transform: translateY(-4px);
}
```

`transform` визуально перемещает элемент, но не меняет место, которое он занимает в потоке.

## Мини-шпаргалка

- Normal flow - базовое расположение элементов.
- Box Model задает размеры и отступы.
- `display` включает модели layout.
- `position` управляет смещением и выпадением из потока.
- `transform` двигает визуально, не перестраивая поток.
- Для основной верстки чаще используют Flexbox/Grid, а не absolute.
