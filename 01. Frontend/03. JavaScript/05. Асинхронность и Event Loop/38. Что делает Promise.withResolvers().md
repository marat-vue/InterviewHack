# Что делает Promise.withResolvers()?

> [!NOTE]
> `Promise.withResolvers()` создает промис и сразу возвращает наружу его `resolve` и `reject`.

## Вопрос

Для чего нужен `Promise.withResolvers()` и чем он отличается от `new Promise()`?

## Определение

`Promise.withResolvers()` - статический метод, который возвращает объект:

```javascript
const { promise, resolve, reject } = Promise.withResolvers();
```

Это удобно, когда промис нужно создать сейчас, а завершить его позже из другого места кода.

## Эквивалент через new Promise

```javascript
let resolve;
let reject;

const promise = new Promise((res, rej) => {
  resolve = res;
  reject = rej;
});
```

`Promise.withResolvers()` делает такой паттерн короче и безопаснее по форме.

## Пример

```javascript
const { promise, resolve, reject } = Promise.withResolvers();

button.addEventListener('click', () => {
  resolve('clicked');
});

promise.then(console.log);
```

Промис завершится, когда пользователь нажмет кнопку.

## Когда использовать

- адаптация callback API к Promise;
- ожидание внешнего события;
- создание очередей;
- ручное управление завершением операции.

## Важный нюанс

Не стоит использовать этот метод везде подряд. Для обычной асинхронной операции чаще достаточно `async/await` или обычного `new Promise()`.

## Мини-шпаргалка

```javascript
const { promise, resolve, reject } = Promise.withResolvers();

resolve(value);
reject(error);
```
