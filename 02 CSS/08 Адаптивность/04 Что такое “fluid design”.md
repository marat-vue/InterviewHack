# Что такое "fluid design"?

> [!NOTE]
> **Fluid design** - это подход, при котором размеры элементов плавно меняются вместе с шириной контейнера или viewport, а не переключаются только в фиксированных точках.

## Главное

Fluid layout часто использует проценты, `fr`, viewport-единицы, `clamp()` и гибкие сетки.

```css
.container {
  width: min(100% - 32px, 1120px);
  margin-inline: auto;
}
```

Контейнер плавно занимает доступную ширину, но не становится шире `1120px`.

## Fluid typography

```css
h1 {
  font-size: clamp(2rem, 5vw, 4rem);
}
```

Размер заголовка плавно меняется между `2rem` и `4rem` в зависимости от viewport.

## Fluid grid

```css
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 16px;
}
```

Колонки перестраиваются без ручного набора breakpoints.

## Отличие от breakpoint-only

```text
breakpoint-only -> размеры меняются скачками
fluid design    -> размеры меняются плавно
```

На практике часто используют оба подхода: fluid-базу и media queries для крупных изменений layout.

## Мини-шпаргалка

- Fluid design плавно реагирует на размер экрана.
- Использует `%`, `fr`, `vw`, `clamp()`, `min()`, `max()`.
- Уменьшает количество жестких breakpoints.
- Хорошо сочетается с Grid и Flexbox.
- Для крупных перестроек layout media queries все равно полезны.
