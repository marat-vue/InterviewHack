# Ошибки в async функциях

> [!NOTE] Коротко
> Ошибки внутри `async`-функции превращаются в rejected Promise, а ошибки из `await` удобно ловить через `try...catch`.

## Вопрос

Как ловить ошибки в `async/await` функциях?

## throw внутри async

```javascript
async function fail() {
  throw new Error('Boom');
}

fail().catch((error) => {
  console.log(error.message); // 'Boom'
});
```

`throw` внутри async-функции отклоняет возвращаемый промис.

## try...catch с await

```javascript
async function loadUser() {
  try {
    const response = await fetch('/api/user');

    if (!response.ok) {
      throw new Error(`HTTP ${response.status}`);
    }

    return await response.json();
  } catch (error) {
    console.error('Failed to load user', error);
    throw error;
  }
}
```

`try...catch` ловит и обычные ошибки, и rejected Promise после `await`.

## Ошибка без await

```javascript
try {
  fail();
} catch (error) {
  console.log('will not catch');
}
```

Такой `catch` не поймает ошибку, потому что `fail()` вернул промис. Нужно `await fail()` или `fail().catch(...)`.

## Правильно

```javascript
try {
  await fail();
} catch (error) {
  console.log(error.message);
}
```

## Мини-шпаргалка

```javascript
try {
  const data = await asyncTask();
} catch (error) {
  handleError(error);
}
```
