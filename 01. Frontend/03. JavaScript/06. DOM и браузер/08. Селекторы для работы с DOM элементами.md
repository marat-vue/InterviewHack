# Селекторы для работы с DOM элементами

> [!NOTE]
> DOM-селекторы позволяют найти элементы на странице, чтобы читать или изменять их через JavaScript.

## Вопрос

Какими методами искать DOM-элементы?

## querySelector()

`querySelector(selector)` возвращает первый элемент, который подходит под CSS-селектор.

```javascript
const button = document.querySelector('.button');
const title = document.querySelector('#title');
const firstItem = document.querySelector('li');
```

Если элемент не найден, метод вернет `null`.

## querySelectorAll()

`querySelectorAll(selector)` возвращает статический `NodeList` со всеми подходящими элементами.

```javascript
const items = document.querySelectorAll('.item');

items.forEach((item) => {
  item.classList.add('active');
});
```

## Старые методы поиска

```javascript
document.getElementById('title');
document.getElementsByClassName('item');
document.getElementsByTagName('li');
```

Они все еще используются, но `querySelector` и `querySelectorAll` чаще удобнее, потому что принимают CSS-селекторы.

## Поиск внутри элемента

```javascript
const card = document.querySelector('.card');
const button = card.querySelector('button');
```

Можно искать не во всем документе, а внутри конкретного контейнера.

## Мини-шпаргалка

```javascript
document.querySelector('.class');     // первый
document.querySelectorAll('.class');  // все
document.getElementById('id');        // по id
```
