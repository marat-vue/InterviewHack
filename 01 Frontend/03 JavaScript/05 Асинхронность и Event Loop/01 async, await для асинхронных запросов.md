# async, await для асинхронных запросов

> [!NOTE] Коротко
> `async/await` - удобный синтаксис поверх `Promise`, который позволяет писать асинхронный код почти как синхронный.

## Вопрос

Какие особенности есть у `async/await` и чем он отличается от работы с промисами через `.then()`?

## Определение

`async` перед функцией означает, что функция всегда возвращает `Promise`. `await` внутри такой функции приостанавливает выполнение текущей async-функции до завершения промиса и возвращает его результат.

`async/await` не заменяет промисы. Он просто дает более читаемый способ работать с ними.

## Promise через then()

```javascript
fetch('/api/user')
  .then((response) => response.json())
  .then((user) => {
    console.log(user.name);
  })
  .catch((error) => {
    console.error(error);
  });
```

## То же самое через async/await

```javascript
async function loadUser() {
  try {
    const response = await fetch('/api/user');
    const user = await response.json();

    console.log(user.name);
  } catch (error) {
    console.error(error);
  }
}
```

Код выглядит линейно: сначала запрос, потом преобразование JSON, потом работа с данными.

## Что возвращает async-функция

```javascript
async function getNumber() {
  return 10;
}

const result = getNumber();

console.log(result); // Promise { 10 }
```

Даже если вернуть обычное значение, оно будет обернуто в промис.

## Последовательность и параллельность

```javascript
// Последовательно: второй запрос ждет первый
const user = await loadUser();
const posts = await loadPosts();

// Параллельно: оба запроса стартуют сразу
const [userData, postsData] = await Promise.all([
  loadUser(),
  loadPosts(),
]);
```

Если операции не зависят друг от друга, лучше запускать их параллельно через `Promise.all()`.

## Мини-шпаргалка

```javascript
async function fn() {}      // всегда возвращает Promise
const value = await promise; // достает fulfilled-значение
try { await task(); } catch (e) {} // обработка ошибок
```
