# Выполнится ли finally, если в try есть return?

> [!NOTE]
> Да, `finally` выполнится перед фактическим выходом из функции, даже если в `try` есть `return`.

## Вопрос

Что произойдет с `finally`, если внутри `try` выполнить `return`?

## Пример

```javascript
function getValue() {
  try {
    return 10;
  } finally {
    console.log('finally');
  }
}

console.log(getValue());
// finally
// 10
```

Сначала выполняется `finally`, затем функция возвращает значение.

## Если есть catch

```javascript
function run() {
  try {
    throw new Error('Boom');
  } catch {
    return 'handled';
  } finally {
    console.log('cleanup');
  }
}

console.log(run());
// cleanup
// handled
```

`finally` выполняется и после `catch`.

## Осторожно: return внутри finally

```javascript
function getValue() {
  try {
    return 1;
  } finally {
    return 2;
  }
}

console.log(getValue()); // 2
```

`return` внутри `finally` перезаписывает предыдущий `return`. Так писать обычно не стоит, потому что это скрывает логику и может потерять ошибку.

## Практическое правило

Используй `finally` для очистки, а не для возврата значений.

## Мини-шпаргалка

```javascript
try {
  return value;
} finally {
  cleanup(); // выполнится перед return
}
```
