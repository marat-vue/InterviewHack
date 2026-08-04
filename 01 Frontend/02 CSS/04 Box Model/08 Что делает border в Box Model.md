# Что делает border в Box Model?

> [!NOTE]
> `border` создает рамку вокруг padding и content элемента. В Box Model он находится между padding и margin.

## Главное

```css
.card {
  border: 1px solid #d1d5db;
}
```

Сокращенное свойство `border` задает ширину, стиль и цвет рамки.

## Состав border

```css
.box {
  border-width: 2px;
  border-style: solid;
  border-color: #2563eb;
}
```

Если не указать `border-style`, рамка обычно не появится.

## Border по сторонам

```css
.tabs {
  border-bottom: 1px solid #e5e7eb;
}
```

Можно задавать рамку отдельно для каждой стороны: `border-top`, `border-right`, `border-bottom`, `border-left`.

## Border и размер

При `content-box` border увеличивает итоговый размер элемента. При `border-box` он входит в `width` и `height`.

```css
.box {
  box-sizing: border-box;
  width: 300px;
  border: 2px solid black;
}
```

## Border-radius

```css
.card {
  border: 1px solid #d1d5db;
  border-radius: 8px;
}
```

`border-radius` скругляет углы border box.

## Мини-шпаргалка

- Border - рамка элемента.
- Находится между padding и margin.
- Состоит из width, style и color.
- Без `border-style` рамка может не отображаться.
- При `border-box` border входит в размер элемента.
- `border-radius` скругляет углы.
