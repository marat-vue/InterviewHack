# Что делает свойство grid-template?

> [!NOTE]
> `grid-template` - это сокращенное свойство для задания строк, колонок и именованных областей CSS Grid.

## Главное

`grid-template` может объединять:

- `grid-template-rows`;
- `grid-template-columns`;
- `grid-template-areas`.

## Пример с rows и columns

```css
.layout {
  display: grid;
  grid-template: auto 1fr auto / 240px 1fr;
}
```

До слеша задаются строки, после слеша - колонки.

```text
rows:    auto 1fr auto
columns: 240px 1fr
```

## Пример с areas

```css
.page {
  display: grid;
  grid-template:
    "header header" auto
    "sidebar main" 1fr
    "footer footer" auto
    / 240px 1fr;
}
```

Так можно одновременно описать области, высоту строк и ширину колонок.

## Когда использовать

`grid-template` удобно для компактного описания layout. Но если запись становится слишком плотной, отдельные свойства читаются лучше.

```css
.page {
  grid-template-areas:
    "header header"
    "sidebar main"
    "footer footer";
  grid-template-columns: 240px 1fr;
  grid-template-rows: auto 1fr auto;
}
```

## Мини-шпаргалка

- `grid-template` сокращает rows, columns и areas.
- До `/` пишут строки, после `/` колонки.
- Может включать именованные области.
- Для сложного layout иногда читабельнее отдельные свойства.
- Не путать с `grid`, который является еще более широким shorthand.
