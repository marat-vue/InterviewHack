# Что такое "grid area"?

> [!NOTE]
> **Grid area** - это прямоугольная область CSS Grid, ограниченная grid lines. Ее можно задать по линиям или назвать через `grid-template-areas`.

## Главное

Grid area может занимать одну или несколько ячеек сетки.

```css
.layout {
  display: grid;
  grid-template-columns: 240px 1fr;
  grid-template-areas:
    "header header"
    "sidebar main"
    "footer footer";
}
```

```css
.header {
  grid-area: header;
}

.sidebar {
  grid-area: sidebar;
}

.main {
  grid-area: main;
}
```

## Именованные области

`grid-template-areas` делает layout визуально читаемым.

```text
"header header"
"sidebar main"
"footer footer"
```

Одинаковые имена рядом образуют одну прямоугольную область.

## Область по линиям

Grid area можно задать и через линии.

```css
.hero {
  grid-column: 1 / 3;
  grid-row: 1 / 2;
}
```

Элемент займет колонки от первой линии до третьей.

## Важное ограничение

Именованная area должна быть прямоугольной.

```css
/* плохо: main образует не прямоугольник */
grid-template-areas:
  "main sidebar"
  "footer main";
```

Такой layout невалиден.

## Мини-шпаргалка

- Grid area - прямоугольная область сетки.
- Ее можно назвать через `grid-template-areas`.
- Элемент помещают в область через `grid-area`.
- Одинаковые имена должны образовывать прямоугольник.
- Area можно задать через `grid-column` и `grid-row`.
