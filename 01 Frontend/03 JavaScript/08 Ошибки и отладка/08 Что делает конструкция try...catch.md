# Что делает конструкция try...catch?

> [!NOTE]
> `try...catch` позволяет поймать исключение и обработать ошибку, чтобы программа не упала полностью.

## Вопрос

Для чего нужна конструкция `try...catch`?

## Определение

Код внутри `try` выполняется обычным образом. Если внутри возникает исключение, выполнение блока `try` прерывается, а управление переходит в `catch`.

## Пример

```javascript
try {
  const data = JSON.parse('{ broken json }');
  console.log(data);
} catch (error) {
  console.error('Invalid JSON:', error.message);
}
```

Ошибка парсинга будет поймана в `catch`.

## Код после ошибки в try не выполняется

```javascript
try {
  console.log('before');
  throw new Error('Boom');
  console.log('after');
} catch (error) {
  console.log(error.message);
}
```

`after` не выведется.

## try...catch и async

```javascript
try {
  const response = await fetch('/api/data');
  const data = await response.json();
} catch (error) {
  console.error(error);
}
```

С `await` можно ловить отклоненные промисы как обычные ошибки.

## Чего try...catch не ловит

Синхронный `try...catch` не поймает ошибку, которая возникла позже в другом callback.

```javascript
try {
  setTimeout(() => {
    throw new Error('Later');
  }, 0);
} catch (error) {
  console.log('will not catch');
}
```

Ошибка возникнет уже после завершения `try`.

## Мини-шпаргалка

```javascript
try {
  riskyCode();
} catch (error) {
  handleError(error);
}
```
