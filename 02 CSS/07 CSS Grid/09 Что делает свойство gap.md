# Что делает свойство gap?

> [!NOTE]
> `gap` задает расстояние между строками и колонками в Grid, Flexbox и некоторых других layout-моделях без добавления margin к самим элементам.

## Главное

```css
.grid {
  display: grid;
  gap: 16px;
}
```

`gap` создает промежутки между grid items.

## Row и column gap

```css
.grid {
  row-gap: 24px;
  column-gap: 16px;
}
```

Сокращенная запись:

```css
.grid {
  gap: 24px 16px;
}
```

Первое значение - строки, второе - колонки.

## Gap во Flexbox

```css
.toolbar {
  display: flex;
  gap: 8px;
}
```

Это проще, чем задавать margin каждому элементу и убирать его у последнего.

## Gap не создает отступ по краям

`gap` добавляет расстояние только между items, но не между item и краем контейнера.

```text
|item gap item gap item|
```

Для отступов от края нужен `padding`.

## Мини-шпаргалка

- `gap` задает расстояние между items.
- Работает в Grid и Flexbox.
- `row-gap` - между строками.
- `column-gap` - между колонками.
- `gap: 24px 16px` = row / column.
- Gap не добавляет внешний отступ по краям контейнера.
