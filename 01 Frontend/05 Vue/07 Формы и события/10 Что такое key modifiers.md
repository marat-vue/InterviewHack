# Что такое key modifiers?

> [!NOTE] Коротко
> Key modifiers позволяют запускать обработчик клавиатурного события только для конкретной клавиши или комбинации клавиш.

## Вопрос

Что такое `key modifiers`?

## Базовый пример

```vue
<input @keyup.enter="submit" />
<input @keyup.esc="close" />
```

Обработчик вызовется только при нужной клавише.

## Частые клавиши

```vue
<input @keydown.enter="submit" />
<input @keydown.tab="focusNext" />
<input @keydown.delete="remove" />
<input @keydown.space="toggle" />
```

## Системные клавиши

```vue
<input @keydown.ctrl.enter="submit" />
<button @click.shift="selectRange">Выбрать диапазон</button>
```

Можно использовать `.ctrl`, `.shift`, `.alt`, `.meta`.

## exact

```vue
<button @click.ctrl.exact="save">Сохранить</button>
```

`.exact` означает, что событие сработает только при указанной комбинации без дополнительных системных клавиш.

## Мини-шпаргалка

- Key modifiers фильтруют события клавиатуры.
- Частые: `.enter`, `.esc`, `.tab`, `.delete`, `.space`.
- Системные: `.ctrl`, `.shift`, `.alt`, `.meta`.
- `.exact` требует точного набора модификаторов.
