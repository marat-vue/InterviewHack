# Что такое Promise?

> [!NOTE] Коротко
> `Promise` - объект, который представляет будущий результат асинхронной операции: успешное значение или ошибку.

## Вопрос

Зачем нужны промисы и как они работают?

## Определение

`Promise` описывает операцию, которая еще не завершилась, но завершится позже. У промиса может быть результат успеха или причина ошибки.

Промисы помогают писать асинхронный код без глубокой вложенности callbacks.

## Создание Promise

```javascript
const promise = new Promise((resolve, reject) => {
  const success = true;

  if (success) {
    resolve('data');
  } else {
    reject(new Error('Something went wrong'));
  }
});
```

`resolve(value)` переводит промис к успешному результату. `reject(reason)` переводит его к ошибке.

## Обработка результата

```javascript
promise
  .then((value) => {
    console.log(value);
  })
  .catch((error) => {
    console.error(error);
  })
  .finally(() => {
    console.log('finished');
  });
```

## Состояния Promise

| Состояние | Значение |
| --- | --- |
| `pending` | ожидание |
| `fulfilled` | успешно выполнен |
| `rejected` | завершен с ошибкой |

После перехода в `fulfilled` или `rejected` промис считается завершенным и больше не меняет состояние.

## Promise и async/await

```javascript
async function loadData() {
  const response = await fetch('/api/data');

  return response.json();
}
```

`async/await` - синтаксис поверх промисов. `await` ждет завершения промиса внутри async-функции.

## Мини-шпаргалка

```javascript
Promise.resolve(value);
Promise.reject(error);
promise.then(onSuccess).catch(onError).finally(onFinally);
```
