# localStorage VS sessionStorage

> [!NOTE] Коротко
> `localStorage` хранит данные между сессиями браузера, а `sessionStorage` очищается при закрытии вкладки.

## Вопрос

Чем `localStorage` отличается от `sessionStorage`?

## Главное отличие

Оба API хранят пары ключ-значение в браузере и работают только со строками. Разница в сроке жизни данных и области доступности.

`localStorage` живет долго: после перезагрузки страницы, закрытия вкладки и даже закрытия браузера.

`sessionStorage` живет только в рамках текущей вкладки.

## Сравнение

| Критерий | `localStorage` | `sessionStorage` |
| --- | --- | --- |
| Срок жизни | пока не удалить вручную | до закрытия вкладки |
| Доступность | все вкладки одного origin | только текущая вкладка |
| Формат данных | строки | строки |
| API | синхронный | синхронный |
| Объем | ограничен браузером | ограничен браузером |

## Пример localStorage

```javascript
localStorage.setItem('theme', 'dark');

console.log(localStorage.getItem('theme')); // 'dark'
```

Тема останется после закрытия браузера.

## Пример sessionStorage

```javascript
sessionStorage.setItem('formStep', '2');

console.log(sessionStorage.getItem('formStep')); // '2'
```

Шаг формы исчезнет после закрытия вкладки.

## Когда что использовать

- `localStorage` - тема, настройки, некритичные предпочтения пользователя;
- `sessionStorage` - временное состояние вкладки, шаг формы, данные текущей сессии.

## Мини-шпаргалка

```javascript
localStorage.setItem('key', 'value');   // надолго
sessionStorage.setItem('key', 'value'); // до закрытия вкладки
```
