# Как избежать callback hell?

> [!NOTE] Коротко
> Callback hell возникает из-за глубокой вложенности асинхронных callbacks. Его избегают декомпозицией, промисами и `async/await`.

## Вопрос

Почему callback hell считается антипаттерном и как его исправить?

## Определение

Callback hell - ситуация, когда один асинхронный callback вложен в другой, затем в третий и так далее. Код превращается в "пирамиду" и становится сложным для чтения, обработки ошибок и изменения.

## Пример проблемы

```javascript
getUser((user) => {
  getPosts(user.id, (posts) => {
    getComments(posts[0].id, (comments) => {
      saveComments(comments, (result) => {
        console.log(result);
      });
    });
  });
});
```

Здесь сложно быстро понять поток данных и обработать ошибку на каждом шаге.

## Почему это плохо

- много уровней вложенности;
- ошибки приходится обрабатывать в каждом callback;
- шаги трудно переиспользовать;
- код сложнее тестировать;
- добавление нового шага делает структуру еще глубже.

## Способ 1: именованные функции

```javascript
function handleComments(comments) {
  saveComments(comments, console.log);
}

function handlePosts(posts) {
  getComments(posts[0].id, handleComments);
}

function handleUser(user) {
  getPosts(user.id, handlePosts);
}

getUser(handleUser);
```

Вложенность уменьшается, но управление ошибками все еще может быть неудобным.

## Способ 2: Promise

```javascript
getUser()
  .then((user) => getPosts(user.id))
  .then((posts) => getComments(posts[0].id))
  .then((comments) => saveComments(comments))
  .then(console.log)
  .catch(console.error);
```

Цепочка становится плоской, а ошибки можно обработать одним `.catch()`.

## Способ 3: async/await

```javascript
async function run() {
  try {
    const user = await getUser();
    const posts = await getPosts(user.id);
    const comments = await getComments(posts[0].id);
    const result = await saveComments(comments);

    console.log(result);
  } catch (error) {
    console.error(error);
  }
}
```

Это обычно самый читаемый вариант для последовательной асинхронной логики.

## Мини-шпаргалка

```javascript
// Лучше глубокой вложенности:
promise
  .then(step1)
  .then(step2)
  .catch(handleError);
```
