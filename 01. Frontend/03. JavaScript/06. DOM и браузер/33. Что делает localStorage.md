# Что делает localStorage?

> [!NOTE]
> `localStorage` хранит пары ключ-значение в браузере без срока истечения, пока данные не удалят вручную.

## Вопрос

Для чего нужен `localStorage` и какие у него ограничения?

## Определение

`localStorage` - браузерное хранилище для строковых данных. Оно привязано к origin сайта и сохраняется между перезагрузками страницы и закрытием браузера.

## Запись и чтение

```javascript
localStorage.setItem('theme', 'dark');

const theme = localStorage.getItem('theme');

console.log(theme); // 'dark'
```

## Удаление

```javascript
localStorage.removeItem('theme');
localStorage.clear();
```

`clear()` удаляет все записи `localStorage` для текущего origin.

## Объекты нужно сериализовать

```javascript
const user = { id: 1, name: 'Ann' };

localStorage.setItem('user', JSON.stringify(user));

const savedUser = JSON.parse(localStorage.getItem('user'));
```

`localStorage` хранит только строки.

## Ограничения

- синхронный API, может блокировать поток при больших данных;
- ограниченный объем;
- нельзя хранить секреты и токены без понимания рисков;
- данные доступны JavaScript-коду на странице.

## Мини-шпаргалка

```javascript
localStorage.setItem(key, value);
localStorage.getItem(key);
localStorage.removeItem(key);
localStorage.clear();
```
