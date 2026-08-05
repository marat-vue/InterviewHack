# Что делает event.target?

> [!NOTE]
> `event.target` указывает на реальный элемент, на котором возникло событие.

## Вопрос

Что хранится в `event.target`?

## Определение

`event.target` - элемент, который стал исходной целью события. Если пользователь кликнул по иконке внутри кнопки, `event.target` может быть именно иконкой, а не кнопкой.

Это особенно важно при всплытии и делегировании событий.

## Пример

```html
<button class="button">
  <span>Save</span>
</button>
```

```javascript
const button = document.querySelector('.button');

button.addEventListener('click', (event) => {
  console.log(event.target); // span, если кликнули по тексту
});
```

Обработчик висит на кнопке, но реальная цель клика может быть вложенным элементом.

## Использование closest()

```javascript
document.addEventListener('click', (event) => {
  const button = event.target.closest('button');

  if (!button) return;

  console.log('button clicked');
});
```

`closest()` помогает найти нужного родителя от фактической цели события.

## target при делегировании

```javascript
list.addEventListener('click', (event) => {
  const item = event.target.closest('[data-id]');

  if (!item) return;

  console.log(item.dataset.id);
});
```

## Мини-шпаргалка

```javascript
event.target; // где событие началось
event.target.closest(selector); // найти подходящего родителя
```
