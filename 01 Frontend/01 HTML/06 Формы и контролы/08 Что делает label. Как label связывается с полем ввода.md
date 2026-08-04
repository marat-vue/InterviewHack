# Что делает label. Как label связывается с полем ввода?

> [!NOTE]
> `<label>` задает подпись для поля формы. Он связывает текст с контролом, улучшает доступность и позволяет фокусировать поле кликом по подписи.

## Главное

Самый явный способ связи - `for` у label и такой же `id` у поля.

```html
<label for="email">Email</label>
<input id="email" name="email" type="email">
```

Скринридер озвучит поле как `Email`, а клик по label переведет фокус в input.

## Вложенный input

Можно вложить поле внутрь label.

```html
<label>
  <input type="checkbox" name="agreement">
  Я согласен с условиями
</label>
```

Так часто делают для чекбоксов и radio.

## Почему placeholder не заменяет label

```html
<!-- хуже -->
<input type="email" placeholder="Email">
```

`placeholder` исчезает при вводе и не всегда достаточно надежно озвучивается assistive technologies. Лучше иметь полноценный label.

```html
<label for="email">Email</label>
<input id="email" type="email" name="email" placeholder="name@example.com">
```

## Label для группы

Для группы radio или checkbox одного label недостаточно. Используют `fieldset` и `legend`.

```html
<fieldset>
  <legend>Способ оплаты</legend>
  <label><input type="radio" name="payment" value="card"> Карта</label>
  <label><input type="radio" name="payment" value="cash"> Наличные</label>
</fieldset>
```

## Мини-шпаргалка

- `label` подписывает поле формы.
- `for` должен совпадать с `id` поля.
- Клик по label фокусирует поле.
- Placeholder не заменяет label.
- Для групп используют `fieldset` и `legend`.
- Хорошие label повышают доступность формы.
