# Что такое border-box?

> [!NOTE]
> `border-box` - это значение `box-sizing`, при котором `width` и `height` включают content, padding и border. Это делает размеры элементов более предсказуемыми.

## Главное

```css
.box {
  box-sizing: border-box;
  width: 300px;
  padding: 20px;
  border: 2px solid black;
}
```

Итоговая ширина элемента останется `300px`. Content area станет меньше, чтобы внутри поместились padding и border.

## Почему удобно

При `border-box` проще строить сетки.

```css
.column {
  box-sizing: border-box;
  width: 50%;
  padding: 24px;
}
```

Две колонки по `50%` остаются в одной строке, потому что padding входит в их ширину.

## Глобальное правило

```css
*,
*::before,
*::after {
  box-sizing: border-box;
}
```

Это одно из самых частых правил в современном CSS-reset.

## Мини-шпаргалка

- `border-box` включает padding и border в `width`.
- Итоговый размер элемента предсказуемее.
- Content area уменьшается при добавлении padding/border.
- Часто задается глобально через `*`.
- Особенно полезен для layout и сеток.
