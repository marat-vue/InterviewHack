# await в обработчике события

> [!NOTE] Коротко
> `await` можно использовать в обработчике события, если обработчик объявлен как `async`.

## Вопрос

Можно ли использовать `await` внутри `addEventListener()`?

## Определение

Обработчик события может быть асинхронной функцией. Для этого перед callback нужно поставить `async`. Тогда внутри можно использовать `await` для запросов, таймеров, промисов и другой асинхронной работы.

## Пример

```javascript
button.addEventListener('click', async () => {
  const response = await fetch('/api/save');
  const result = await response.json();

  console.log(result);
});
```

## Обработка ошибок

Ошибки внутри async-обработчика нужно ловить явно.

```javascript
button.addEventListener('click', async () => {
  try {
    const response = await fetch('/api/save');

    if (!response.ok) {
      throw new Error('Save failed');
    }

    console.log('Saved');
  } catch (error) {
    console.error(error);
  }
});
```

## Важный нюанс

Браузер не ждет промис, который вернул обработчик события. Если внутри произойдет ошибка и ее не поймать, можно получить необработанный rejected Promise.

## UI-состояние

```javascript
button.addEventListener('click', async () => {
  button.disabled = true;

  try {
    await saveData();
  } finally {
    button.disabled = false;
  }
});
```

`finally` удобен, чтобы вернуть интерфейс в нормальное состояние.

## Мини-шпаргалка

```javascript
element.addEventListener('click', async (event) => {
  try {
    await task();
  } catch (error) {
    handleError(error);
  }
});
```
