# Что делает оператор throw?

> [!NOTE] Коротко
> `throw` выбрасывает исключение и немедленно прерывает выполнение текущего потока кода.

## Вопрос

Что делает оператор `throw` в JavaScript?

## Определение

`throw expression` выбрасывает значение как исключение. После `throw` код ниже в текущем блоке не выполняется, а движок ищет ближайший `catch`.

Обычно выбрасывают объект `Error`.

## Пример

```javascript
function getUser(id) {
  if (!id) {
    throw new Error('User id is required');
  }

  return { id };
}
```

Если `id` не передан, функция остановится на `throw`.

## Обработка

```javascript
try {
  getUser();
} catch (error) {
  console.error(error.message); // 'User id is required'
}
```

## Можно выбросить любое значение

```javascript
throw 'Something went wrong';
```

Так делать не рекомендуется: строка не имеет `stack`, `name` и привычной структуры ошибки.

Лучше:

```javascript
throw new Error('Something went wrong');
```

## Мини-шпаргалка

```javascript
if (!condition) {
  throw new Error('Message');
}
```
