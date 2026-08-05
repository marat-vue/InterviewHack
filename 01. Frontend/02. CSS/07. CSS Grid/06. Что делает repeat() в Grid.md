# Что делает repeat() в Grid?

> [!NOTE]
> `repeat()` в CSS Grid сокращает запись повторяющихся строк или колонок. Вместо ручного перечисления одинаковых треков можно указать количество повторений и шаблон.

## Главное

```css
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
```

Это то же самое, что:

```css
.grid {
  grid-template-columns: 1fr 1fr 1fr;
}
```

## Повторение сложного шаблона

```css
.grid {
  grid-template-columns: repeat(2, 100px 1fr);
}
```

Результат:

```text
100px 1fr 100px 1fr
```

## auto-fit и auto-fill

```css
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 16px;
}
```

Браузер сам вычисляет, сколько колонок помещается.

## Когда использовать

- Равные колонки.
- Повторяющиеся ритмы сетки.
- Адаптивные карточки.
- Сетки с `auto-fit` или `auto-fill`.

## Мини-шпаргалка

- `repeat(3, 1fr)` создает три одинаковых трека.
- Можно повторять сложный шаблон.
- `auto-fit` и `auto-fill` делают сетку адаптивнее.
- `repeat()` работает в columns и rows.
- Частый паттерн: `repeat(auto-fit, minmax(...))`.
