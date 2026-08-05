# Что делает history объект?

> [!NOTE]
> `history` управляет историей навигации вкладки: переходами назад, вперед и изменением URL без перезагрузки страницы.

## Вопрос

Что делает объект `history` в браузере?

## Определение

`history` - объект браузера, связанный с историей текущей вкладки. Он позволяет программно перейти назад или вперед, а также добавить или заменить запись истории.

SPA-приложения используют History API, чтобы менять URL без полной перезагрузки страницы.

## Навигация

```javascript
history.back();    // назад
history.forward(); // вперед
history.go(-2);    // на две записи назад
```

## pushState()

```javascript
history.pushState(
  { page: 'profile' },
  '',
  '/profile'
);
```

`pushState()` добавляет новую запись в историю и меняет URL без перезагрузки.

## replaceState()

```javascript
history.replaceState(
  { page: 'settings' },
  '',
  '/settings'
);
```

`replaceState()` заменяет текущую запись истории.

## Событие popstate

```javascript
window.addEventListener('popstate', (event) => {
  console.log(event.state);
});
```

`popstate` срабатывает при переходе по истории, например когда пользователь нажал "назад".

## Мини-шпаргалка

```javascript
history.pushState(state, '', url);
history.replaceState(state, '', url);
history.back();
```
