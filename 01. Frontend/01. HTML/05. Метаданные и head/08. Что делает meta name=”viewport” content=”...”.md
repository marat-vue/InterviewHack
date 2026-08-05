# Что делает meta name="viewport" content="..."?

> [!NOTE]
> `<meta name="viewport">` управляет тем, как страница масштабируется и отображается на мобильных устройствах. Без него адаптивная верстка может выглядеть как уменьшенная desktop-страница.

## Главное

Самая частая запись:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

Она говорит браузеру: ширина viewport должна соответствовать ширине устройства, а начальный масштаб равен `1`.

## Что такое viewport

Viewport - это область, в которой браузер отображает страницу. На мобильных устройствах без meta viewport браузер может использовать виртуальную ширину вроде desktop-экрана, а затем уменьшать страницу.

```text
without viewport meta:
  layout width may be desktop-like
  page is scaled down

with viewport meta:
  layout width matches device width
  responsive CSS works as expected
```

## Разбор content

```html
content="width=device-width, initial-scale=1.0"
```

- `width=device-width` - использовать реальную ширину устройства.
- `initial-scale=1.0` - начальный масштаб без уменьшения или увеличения.

## Почему это важно для CSS

Media queries рассчитываются относительно viewport.

```css
@media (max-width: 600px) {
  .layout {
    grid-template-columns: 1fr;
  }
}
```

Без корректного viewport мобильная media query может сработать не так, как ожидается.

## Чего избегать

Не стоит запрещать масштабирование пользователю.

```html
<!-- плохо для доступности -->
<meta
  name="viewport"
  content="width=device-width, initial-scale=1.0, user-scalable=no"
>
```

Пользователи с ослабленным зрением должны иметь возможность увеличить страницу.

## Мини-шпаргалка

- `viewport` нужен для адаптивной верстки.
- Обычно используют `width=device-width, initial-scale=1.0`.
- Он особенно важен на мобильных устройствах.
- Media queries зависят от viewport.
- Не запрещай масштабирование без крайней необходимости.
