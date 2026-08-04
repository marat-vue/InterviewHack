# Что такое Box Model в CSS. Из каких частей состоит Box Model?

> [!NOTE]
> **Box Model** - это модель, по которой браузер рассчитывает размер и пространство вокруг элемента. Каждый элемент можно представить как прямоугольник из content, padding, border и margin.

## Состав Box Model

```text
margin
  border
    padding
      content
```

| Часть | Что означает |
| --- | --- |
| `content` | Содержимое элемента: текст, изображение, дочерние элементы |
| `padding` | Внутренний отступ между content и border |
| `border` | Рамка вокруг padding и content |
| `margin` | Внешний отступ между элементом и соседями |

## Пример

```css
.card {
  width: 300px;
  padding: 16px;
  border: 1px solid #d1d5db;
  margin: 24px;
}
```

Как именно `width` будет считаться, зависит от `box-sizing`.

## content-box и border-box

```css
.box {
  box-sizing: content-box;
}
```

При `content-box` ширина `width` относится только к content.

```css
.box {
  box-sizing: border-box;
}
```

При `border-box` ширина включает content, padding и border.

## Мини-шпаргалка

- Box Model описывает размер элемента.
- Content - содержимое.
- Padding - внутренний отступ.
- Border - рамка.
- Margin - внешний отступ.
- `box-sizing` меняет способ расчета ширины и высоты.
