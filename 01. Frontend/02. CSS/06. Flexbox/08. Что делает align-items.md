# Что делает align-items?

> [!NOTE]
> `align-items` выравнивает flex items по cross axis внутри flex-линии: в начало, центр, конец, растягивание или по базовой линии текста.

## Главное

```css
.toolbar {
  display: flex;
  align-items: center;
}
```

Элементы выровняются по поперечной оси.

## Cross axis

При `flex-direction: row` cross axis вертикальная.

```css
.row {
  display: flex;
  align-items: center;
}
```

При `flex-direction: column` cross axis горизонтальная.

## Частые значения

| Значение | Поведение |
| --- | --- |
| `stretch` | Растянуть items по cross axis |
| `flex-start` | Прижать к началу cross axis |
| `center` | Центрировать |
| `flex-end` | Прижать к концу |
| `baseline` | Выровнять по базовой линии текста |

## Пример

```css
.media {
  display: flex;
  align-items: center;
  gap: 12px;
}
```

```html
<div class="media">
  <img src="/avatar.jpg" alt="Анна" width="40" height="40">
  <span>Анна Иванова</span>
</div>
```

Аватар и текст будут выровнены по центру по вертикали.

## Мини-шпаргалка

- `align-items` работает по cross axis.
- При `row` это обычно вертикаль.
- При `column` это обычно горизонталь.
- Значение по умолчанию часто `stretch`.
- Для одного элемента используют `align-self`.
