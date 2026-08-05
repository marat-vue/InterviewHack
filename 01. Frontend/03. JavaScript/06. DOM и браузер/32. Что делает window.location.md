# Что делает window.location?

> [!NOTE]
> `window.location` хранит текущий URL страницы и позволяет перейти на другой адрес или перезагрузить страницу.

## Вопрос

Что можно делать через `window.location`?

## Определение

`window.location` - объект браузера с информацией о текущем адресе. Через него можно читать части URL и управлять навигацией.

## Чтение URL

```javascript
console.log(location.href);
console.log(location.origin);
console.log(location.pathname);
console.log(location.search);
console.log(location.hash);
```

## Переход на другой URL

```javascript
location.href = '/profile';
```

Такой переход добавит новую запись в историю.

## assign() и replace()

```javascript
location.assign('/profile');
location.replace('/login');
```

`assign()` похож на присваивание `href`. `replace()` заменяет текущую запись истории, поэтому пользователь не вернется на старую страницу кнопкой "назад".

## Перезагрузка

```javascript
location.reload();
```

## location vs history

`location` отвечает за текущий URL и навигацию. `history` управляет записями истории и позволяет менять URL в SPA через `pushState()` без перезагрузки.

## Мини-шпаргалка

```javascript
location.href;
location.pathname;
location.assign(url);
location.replace(url);
location.reload();
```
