# Чем CSS Grid отличается от Flexbox?

> [!NOTE]
> Flexbox лучше подходит для одномерного layout вдоль одной оси, а CSS Grid - для двумерных сеток, где нужно управлять строками и колонками одновременно.

## Главное

```text
Flexbox -> row or column
Grid    -> rows and columns
```

Flexbox думает от контента: items распределяются вдоль оси. Grid думает от сетки: сначала задается структура, затем элементы размещаются в ней.

## Flexbox

```css
.toolbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
```

Хорош для:

- меню;
- тулбаров;
- строк кнопок;
- media object;
- равномерного распределения items;
- простых адаптивных карточек.

## Grid

```css
.layout {
  display: grid;
  grid-template-columns: 240px 1fr;
  grid-template-areas: "sidebar content";
}
```

Хорош для:

- страниц с зонами;
- dashboard;
- галерей;
- сложных карточных сеток;
- таблицеподобных layout;
- управления строками и колонками вместе.

## Можно использовать вместе

```css
.page {
  display: grid;
  grid-template-columns: 240px 1fr;
}

.toolbar {
  display: flex;
  justify-content: space-between;
}
```

Grid может управлять крупным layout, а Flexbox - внутренним выравниванием компонентов.

## Мини-шпаргалка

- Flexbox - одномерный layout.
- Grid - двумерный layout.
- Flexbox удобен для выравнивания items.
- Grid удобен для структуры страницы.
- Их нормально комбинировать.
- Не выбирай один инструмент навсегда: выбирай по задаче.
