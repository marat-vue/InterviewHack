# Что делает свойство display?

> [!NOTE]
> `display` определяет, как элемент участвует в layout: является ли он блоком, inline-элементом, flex-контейнером, grid-контейнером или вообще не отображается.

## Главное

```css
.layout {
  display: flex;
}
```

Свойство `display` влияет и на поведение самого элемента, и иногда на layout его детей.

## Частые значения

| Значение | Что делает |
| --- | --- |
| `block` | Элемент занимает строку как блок |
| `inline` | Элемент идет внутри строки |
| `inline-block` | Inline-снаружи, block-внутри |
| `flex` | Включает Flexbox для детей |
| `grid` | Включает CSS Grid для детей |
| `none` | Убирает элемент из отображения и layout |

## block и inline

```css
a {
  display: inline;
}

section {
  display: block;
}
```

Семантика HTML и `display` - разные вещи: ссылку можно сделать блочной, но она останется ссылкой.

## display none

```css
.modal {
  display: none;
}
```

Элемент не занимает место и обычно недоступен для скринридеров.

## Flex и Grid

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

Flexbox чаще удобен для одномерного layout, Grid - для двумерного.

## Мини-шпаргалка

- `display` задает модель отображения.
- `block` занимает доступную ширину.
- `inline` находится в строке.
- `flex` и `grid` управляют детьми.
- `display: none` убирает элемент из layout.
- Не выбирай HTML-тег только из-за дефолтного display.
