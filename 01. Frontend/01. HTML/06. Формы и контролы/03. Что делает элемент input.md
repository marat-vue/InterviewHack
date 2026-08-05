# Что делает элемент input?

> [!NOTE]
> `<input>` - универсальный элемент формы для ввода данных. Его поведение зависит от атрибута `type`: текст, email, пароль, чекбокс, radio, файл, дата и другие варианты.

## Главное

```html
<label for="email">Email</label>
<input id="email" name="email" type="email" required>
```

`input` собирает значение пользователя, а браузер может валидировать его в зависимости от типа.

## Частые type

| Type | Назначение |
| --- | --- |
| `text` | Обычный текст |
| `email` | Email с базовой проверкой |
| `password` | Пароль, скрывает ввод |
| `number` | Числовой ввод |
| `checkbox` | Независимый флажок |
| `radio` | Выбор одного варианта из группы |
| `file` | Загрузка файла |
| `search` | Поле поиска |
| `date` | Выбор даты |
| `hidden` | Скрытое значение формы |

## Атрибуты input

```html
<input
  id="username"
  name="username"
  type="text"
  placeholder="marat_dev"
  minlength="3"
  maxlength="20"
  autocomplete="username"
  required
>
```

Полезные атрибуты:

- `name` - имя поля при отправке;
- `value` - текущее или начальное значение;
- `placeholder` - подсказка, но не замена `label`;
- `required` - обязательное поле;
- `disabled` - отключенное поле;
- `readonly` - поле только для чтения;
- `autocomplete` - подсказки автозаполнения.

## Input и label

```html
<label for="phone">Телефон</label>
<input id="phone" name="phone" type="tel">
```

Связка `label` + `input` улучшает доступность и увеличивает кликабельную область.

## Мини-шпаргалка

- `input` создает поле ввода.
- Поведение зависит от `type`.
- Для отправки данных нужен `name`.
- `placeholder` не заменяет `label`.
- `required`, `minlength`, `pattern` помогают HTML-валидации.
- Для загрузки файла используют `type="file"`.
