# Что такое key modifiers?

> [!NOTE]
> Key modifiers - модификаторы событий клавиатуры, которые позволяют вызывать обработчик только при нажатии конкретной клавиши, например `@keyup.enter`.

## Вопрос

Что такое `key modifiers`?

## Базовый пример

```vue
<template>
  <input @keyup.enter="submit" />
  <input @keyup.esc="close" />
</template>
```

`submit` вызовется только при `Enter`, а `close` - только при `Escape`.

## Частые клавиши

```vue
<input @keyup.enter="submit" />
<input @keyup.tab="focusNext" />
<input @keyup.delete="remove" />
<input @keyup.esc="close" />
<input @keyup.space="toggle" />
```

## Системные модификаторы

Можно сочетать клавиши с `ctrl`, `shift`, `alt`, `meta`.

```vue
<input @keydown.ctrl.enter="submit" />
<button @click.shift="selectRange">Выбрать диапазон</button>
```

## Exact

`.exact` требует, чтобы были нажаты только указанные модификаторы.

```vue
<button @click.ctrl.exact="save">Ctrl + click</button>
```

## Мини-шпаргалка

- Key modifiers фильтруют события клавиатуры.
- Частые: `.enter`, `.esc`, `.tab`, `.delete`, `.space`.
- Можно сочетать с `.ctrl`, `.shift`, `.alt`, `.meta`.
- `.exact` запрещает лишние системные клавиши.
