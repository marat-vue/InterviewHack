# Атрибуты vs свойства у DOM элемента

> [!NOTE] Коротко
> Атрибуты находятся в HTML-разметке, а свойства находятся у DOM-объекта в JavaScript.

## Вопрос

Чем атрибуты отличаются от свойств DOM-элемента?

## Определение

Атрибут - значение в HTML:

```html
<input id="name" value="Ann">
```

Свойство - значение у DOM-объекта:

```javascript
const input = document.querySelector('#name');

console.log(input.value);
```

Часто атрибут и свойство связаны, но это не одно и то же.

## Пример с input value

```javascript
const input = document.querySelector('#name');

input.value = 'Bob';

console.log(input.getAttribute('value')); // 'Ann'
console.log(input.value);                 // 'Bob'
```

Атрибут `value` хранит начальное значение из HTML, а свойство `value` отражает текущее значение поля.

## Работа с атрибутами

```javascript
element.getAttribute('href');
element.setAttribute('aria-label', 'Close');
element.removeAttribute('hidden');
element.hasAttribute('disabled');
```

## Работа со свойствами

```javascript
input.value = 'Text';
button.disabled = true;
image.src = '/image.png';
```

## Сравнение

| Атрибут | Свойство |
| --- | --- |
| часть HTML | часть DOM-объекта |
| обычно строка | может быть любым типом |
| задает начальное состояние | отражает текущее состояние |
| `getAttribute()` | `element.property` |

## Мини-шпаргалка

```javascript
element.getAttribute('data-id');
element.setAttribute('disabled', '');
button.disabled = true;
input.value = 'new value';
```
