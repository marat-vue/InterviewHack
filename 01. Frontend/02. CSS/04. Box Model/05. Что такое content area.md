# Что такое content area?

> [!NOTE]
> **Content area** - это внутренняя область элемента, где находится его содержимое: текст, изображения, inline-контент или дочерние элементы.

## Главное

Content area - центральная часть Box Model.

```text
margin
  border
    padding
      content area
```

Именно для content area при `box-sizing: content-box` задаются `width` и `height`.

## Пример

```css
.box {
  box-sizing: content-box;
  width: 300px;
  height: 120px;
  padding: 20px;
  border: 2px solid black;
}
```

Здесь content area имеет размер `300x120`, а итоговый border box будет больше.

## При border-box

```css
.box {
  box-sizing: border-box;
  width: 300px;
  padding: 20px;
}
```

Теперь `300px` - это весь border box, а content area станет меньше из-за padding.

## Что происходит с переполнением

Если содержимого больше, чем помещается в content area, возникает overflow.

```css
.box {
  width: 200px;
  height: 100px;
  overflow: auto;
}
```

## Мини-шпаргалка

- Content area содержит реальный контент.
- Это центр Box Model.
- При `content-box` width/height задают content area.
- При `border-box` content area уменьшается из-за padding и border.
- Если контент не помещается, возникает overflow.
