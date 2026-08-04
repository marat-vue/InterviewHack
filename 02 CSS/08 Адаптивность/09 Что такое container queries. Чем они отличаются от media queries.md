# Что такое container queries. Чем они отличаются от media queries?

> [!NOTE]
> **Container queries** позволяют менять стили элемента в зависимости от размера его контейнера, а не всего viewport. Это особенно полезно для переиспользуемых компонентов.

## Главное

Media query смотрит на viewport.

```css
@media (min-width: 768px) {
  .card {
    display: grid;
  }
}
```

Container query смотрит на контейнер компонента.

```css
.card-wrapper {
  container-type: inline-size;
}

@container (min-width: 480px) {
  .card {
    display: grid;
    grid-template-columns: 160px 1fr;
  }
}
```

## Зачем это нужно

Один и тот же компонент может жить в разных местах: в широкой колонке, узком сайдбаре, модалке или карточной сетке. Размер viewport при этом одинаковый, а доступное место компонента разное.

```text
viewport: 1440px
  main content card: wide
  sidebar card: narrow
```

Media query не знает, насколько широк конкретный контейнер. Container query знает.

## Как включить

На родителе нужно создать container.

```css
.product-card-shell {
  container-type: inline-size;
}
```

После этого внутри можно писать `@container`.

```css
@container (min-width: 520px) {
  .product-card {
    grid-template-columns: auto 1fr;
  }
}
```

## Media queries vs container queries

| Инструмент | От чего зависит | Когда использовать |
| --- | --- | --- |
| Media query | Viewport или характеристики устройства | Общий layout страницы |
| Container query | Размер контейнера | Переиспользуемые компоненты |

## Мини-шпаргалка

- Media query смотрит на viewport.
- Container query смотрит на контейнер.
- Для container query нужно задать `container-type`.
- Хорошо подходит для компонентов.
- Не заменяет media queries полностью.
- Часто используют вместе: media для страницы, container для компонентов.
