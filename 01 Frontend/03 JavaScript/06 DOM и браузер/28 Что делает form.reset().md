# Что делает form.reset()?

> [!NOTE] Коротко
> `form.reset()` сбрасывает поля формы к их начальным значениям из HTML.

## Вопрос

Что делает метод `reset()` у формы?

## Определение

`form.reset()` возвращает элементы формы к исходному состоянию: значениям, которые были заданы в HTML через `value`, `checked`, `selected` и похожие атрибуты.

Он не очищает форму "до пустоты", если у полей были начальные значения.

## Пример

```html
<form id="profile">
  <input name="name" value="Ann">
  <input name="agree" type="checkbox" checked>
</form>
```

```javascript
const form = document.querySelector('#profile');

form.elements.name.value = 'Bob';
form.elements.agree.checked = false;

form.reset();

console.log(form.elements.name.value); // 'Ann'
console.log(form.elements.agree.checked); // true
```

## Событие reset

```javascript
form.addEventListener('reset', () => {
  console.log('form was reset');
});
```

Событие `reset` можно отследить и при необходимости отменить через `preventDefault()`.

## Когда использовать

- кнопка "Очистить";
- возврат формы к начальному состоянию;
- сброс после успешной отправки;
- отмена редактирования.

## Мини-шпаргалка

```javascript
form.reset(); // вернуть начальные значения
```
