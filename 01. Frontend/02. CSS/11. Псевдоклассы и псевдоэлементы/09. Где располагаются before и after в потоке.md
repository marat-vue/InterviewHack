# Где располагаются before и after в потоке?

> [!NOTE]
> `::before` и `::after` создаются внутри выбранного элемента: `::before` располагается перед содержимым, а `::after` - после него. По умолчанию они участвуют в inline-потоке, если не изменить `display` или `position`.

## Главное

```html
<span class="badge">Новое</span>
```

```css
.badge::before {
  content: "[";
}

.badge::after {
  content: "]";
}
```

Визуально получится:

```text
[Новое]
```

## Упрощенная структура

```text
element
  ::before
  real content
  ::after
```

Псевдоэлементы не появляются как реальные DOM-узлы, но в визуальном форматировании ведут себя как часть элемента.

## По умолчанию inline

```css
.tag::before {
  content: "#";
}
```

Такой `::before` будет идти в строке перед текстом.

## Можно сделать block

```css
.card::before {
  content: "";
  display: block;
  height: 4px;
  background: #2563eb;
}
```

Теперь псевдоэлемент занимает отдельную строку внутри карточки перед содержимым.

## Абсолютное позиционирование

```css
.card {
  position: relative;
}

.card::before {
  content: "";
  position: absolute;
  inset: 0;
  border: 2px solid #2563eb;
  pointer-events: none;
}
```

При `position: absolute` псевдоэлемент выпадает из обычного потока, как обычный absolutely positioned элемент.

## Мини-шпаргалка

- `::before` находится перед содержимым элемента.
- `::after` находится после содержимого элемента.
- По умолчанию они ведут себя как inline.
- `display` может сделать их block/flex/grid.
- `position: absolute` выводит их из потока.
- В DOM они не появляются как отдельные HTML-элементы.
