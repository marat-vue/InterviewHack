# Как активировать flexbox для контейнера?

> [!NOTE]
> Flexbox активируется свойством `display: flex` или `display: inline-flex` на контейнере. Его прямые дочерние элементы становятся flex items.

## Главное

```css
.menu {
  display: flex;
}
```

```html
<nav class="menu">
  <a href="/">Главная</a>
  <a href="/catalog">Каталог</a>
  <a href="/contacts">Контакты</a>
</nav>
```

Только прямые дети `.menu` становятся flex items.

## display flex

```css
.toolbar {
  display: flex;
  gap: 12px;
}
```

Контейнер ведет себя как блочный элемент, а его дети раскладываются по flex-правилам.

## inline-flex

```css
.badge-list {
  display: inline-flex;
  gap: 4px;
}
```

`inline-flex` включает flex внутри, но сам контейнер ведет себя снаружи как inline-level элемент.

## Прямые дети

```html
<div class="wrapper">
  <div class="inner">
    <button>Один</button>
    <button>Два</button>
  </div>
</div>
```

Если `display: flex` стоит на `.wrapper`, flex item будет `.inner`, а не кнопки. Чтобы управлять кнопками, flex нужно поставить на `.inner`.

## Мини-шпаргалка

- Flexbox включается через `display: flex`.
- `inline-flex` делает контейнер inline-level снаружи.
- Flex items - только прямые дети контейнера.
- Для расстояний между элементами используй `gap`.
- После включения flex можно управлять осями и выравниванием.
