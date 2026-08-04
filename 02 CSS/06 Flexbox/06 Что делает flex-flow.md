# Что делает flex-flow?

> [!NOTE]
> `flex-flow` - это сокращенное свойство для `flex-direction` и `flex-wrap`. Оно задает направление flex-оси и разрешает или запрещает перенос элементов.

## Главное

```css
.cards {
  display: flex;
  flex-flow: row wrap;
}
```

Это то же самое, что:

```css
.cards {
  flex-direction: row;
  flex-wrap: wrap;
}
```

## Порядок значений

Обычно сначала пишут direction, затем wrap.

```css
.stack {
  flex-flow: column nowrap;
}
```

Но CSS может распознать значения и в другом порядке, если они однозначны.

## Частые варианты

```css
.toolbar {
  flex-flow: row nowrap;
}

.tag-list {
  flex-flow: row wrap;
}

.sidebar {
  flex-flow: column nowrap;
}
```

## Когда использовать

`flex-flow` удобно, если нужно явно задать оба параметра в одной строке. Если меняется только перенос или только направление, отдельные свойства могут читаться лучше.

## Мини-шпаргалка

- `flex-flow` = `flex-direction` + `flex-wrap`.
- Пример: `flex-flow: row wrap`.
- Direction задает main axis.
- Wrap задает перенос линий.
- Сокращение удобно для краткой записи layout.
