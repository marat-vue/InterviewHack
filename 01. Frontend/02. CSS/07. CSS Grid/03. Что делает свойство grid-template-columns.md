# Что делает свойство grid-template-columns?

> [!NOTE]
> `grid-template-columns` задает структуру колонок в CSS Grid: их количество, размеры и иногда имена grid lines.

## Главное

```css
.layout {
  display: grid;
  grid-template-columns: 240px 1fr;
}
```

Сетка получит две колонки: первая фиксированная `240px`, вторая занимает оставшееся пространство.

## Несколько колонок

```css
.gallery {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 16px;
}
```

Три равные колонки.

## repeat()

```css
.gallery {
  grid-template-columns: repeat(3, 1fr);
}
```

То же самое, но короче.

## Адаптивная сетка

```css
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 16px;
}
```

Браузер сам подберет количество колонок, которые помещаются в контейнер.

## Именованные линии

```css
.layout {
  grid-template-columns: [sidebar-start] 240px [sidebar-end content-start] 1fr [content-end];
}
```

Имена линий помогают размещать элементы понятнее.

## Мини-шпаргалка

- `grid-template-columns` задает колонки.
- Можно использовать `px`, `%`, `fr`, `minmax()`.
- `repeat()` сокращает повторяющиеся треки.
- `auto-fit` и `auto-fill` помогают адаптивным сеткам.
- Именованные линии улучшают читаемость сложного layout.
