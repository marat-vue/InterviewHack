# Что делает свойство z-index?

> [!NOTE]
> `z-index` управляет порядком наложения элементов по оси Z. Он помогает определить, какой элемент окажется выше, если элементы перекрывают друг друга.

## Главное

```css
.modal {
  position: fixed;
  z-index: 1000;
}
```

`z-index` работает для позиционированных элементов и элементов внутри некоторых layout-контекстов, но его поведение зависит от stacking context.

## Пример

```css
.card {
  position: relative;
}

.card__badge {
  position: absolute;
  z-index: 2;
}
```

Бейдж окажется выше других слоев внутри карточки.

## Stacking context

Главный нюанс: `z-index` сравнивается не всегда глобально. Если элемент находится внутри stacking context, он не может просто перепрыгнуть элементы из другого контекста.

Stacking context могут создавать:

- `position` + `z-index`;
- `opacity` меньше `1`;
- `transform`;
- `filter`;
- `isolation: isolate`;
- некоторые значения `contain` и `will-change`.

## Почему z-index "не работает"

```css
.parent {
  transform: translateZ(0);
}

.child {
  position: absolute;
  z-index: 9999;
}
```

Если `.parent` создал stacking context, ребенок ограничен этим контекстом. Большой `z-index` не гарантирует победу над всем интерфейсом.

## Практический подход

В дизайн-системах часто заводят шкалу слоев.

```css
:root {
  --z-dropdown: 100;
  --z-sticky: 200;
  --z-modal: 1000;
  --z-toast: 1100;
}
```

## Мини-шпаргалка

- `z-index` управляет наложением.
- Часто требует `position`.
- Stacking context ограничивает сравнение слоев.
- Большое число не всегда решает проблему.
- Для проекта полезна шкала z-index.
- `transform` и `opacity` могут создавать новые контексты.
