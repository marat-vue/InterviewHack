# Что делает position relative?

> [!NOTE]
> `position: relative` оставляет элемент в нормальном потоке документа, но позволяет визуально смещать его через `top`, `right`, `bottom`, `left` и создавать containing block для абсолютно позиционированных потомков.

## Главное

```css
.badge-anchor {
  position: relative;
}
```

Сам элемент остается на своем месте в layout.

## Визуальное смещение

```css
.box {
  position: relative;
  top: 8px;
  left: 12px;
}
```

Элемент визуально сместится вниз и вправо, но место в потоке останется там, где было изначально.

## Containing block для absolute

Самый частый сценарий `relative` - сделать родителя точкой отсчета для `absolute`-потомка.

```css
.card {
  position: relative;
}

.card__badge {
  position: absolute;
  top: 8px;
  right: 8px;
}
```

```html
<article class="card">
  <span class="card__badge">New</span>
  <h2>Товар</h2>
</article>
```

Бейдж будет позиционироваться относительно карточки.

## Relative и z-index

Позиционированный элемент может участвовать в управлении слоями через `z-index`.

```css
.header {
  position: relative;
  z-index: 10;
}
```

## Мини-шпаргалка

- `relative` сохраняет место элемента в потоке.
- `top/right/bottom/left` смещают элемент визуально.
- Исходное место элемента остается занятым.
- Часто используется как anchor для `position: absolute`.
- Позволяет применять `z-index`.
