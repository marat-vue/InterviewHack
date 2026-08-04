# Что делают data-атрибуты и какая у них задача?

> [!NOTE]
> `data-*` атрибуты позволяют хранить пользовательские данные прямо в HTML-разметке. Они полезны для JS-хуков, тестов, идентификаторов и небольших настроек элемента.

## Главное

Любой атрибут, начинающийся с `data-`, считается пользовательским data-атрибутом.

```html
<button
  type="button"
  data-product-id="42"
  data-action="add-to-cart"
>
  Купить
</button>
```

Браузер не придает этим данным встроенного смысла, но JavaScript может их читать.

## Доступ через dataset

```js
const button = document.querySelector("button");

console.log(button.dataset.productId); // "42"
console.log(button.dataset.action);    // "add-to-cart"
```

Имя `data-product-id` превращается в `dataset.productId`.

## Для чего используют

- Идентификаторы сущностей: `data-user-id`, `data-product-id`.
- JS-действия: `data-action`.
- Тестовые селекторы: `data-test`, `data-testid`.
- Небольшие настройки компонентов.
- Интеграции с аналитикой.

```html
<button data-test="save-button" type="submit">
  Сохранить
</button>
```

Тестовый селектор не зависит от CSS-классов и текста кнопки.

## Чего не стоит делать

Не нужно превращать HTML в базу данных.

```html
<!-- слишком много данных для атрибутов -->
<div data-user='{"id":1,"name":"Анна","roles":["admin"]}'></div>
```

Для сложных данных лучше использовать JavaScript-состояние, JSON-скрипт или API.

## Мини-шпаргалка

- `data-*` хранит пользовательские данные на элементе.
- В JS доступен через `element.dataset`.
- `data-product-id` становится `dataset.productId`.
- Удобен для тестов и небольших JS-хуков.
- Не стоит хранить в data-атрибутах большие сложные объекты.
