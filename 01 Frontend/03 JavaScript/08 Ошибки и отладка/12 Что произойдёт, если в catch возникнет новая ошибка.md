# Что произойдёт, если в catch возникнет новая ошибка?

> [!NOTE] Коротко
> Если внутри `catch` возникнет новая ошибка, она будет выброшена дальше и должна быть обработана внешним `try...catch`.

## Вопрос

Что будет, если обработчик ошибки сам упадет?

## Определение

`catch` - обычный блок кода. Внутри него тоже могут возникать ошибки. Если такая ошибка не обработана внутри самого `catch`, она прерывает выполнение и поднимается выше по стеку.

## Пример

```javascript
try {
  throw new Error('Original error');
} catch (error) {
  console.log(error.message);
  throw new Error('Error inside catch');
}
```

Новая ошибка заменит текущий поток выполнения и станет необработанной, если снаружи нет еще одного `catch`.

## Внешний catch

```javascript
try {
  try {
    throw new Error('Original error');
  } catch {
    throw new Error('Handler failed');
  }
} catch (error) {
  console.log(error.message); // 'Handler failed'
}
```

Внешний `catch` ловит ошибку, возникшую во внутреннем `catch`.

## Как сохранить исходную причину

```javascript
try {
  riskyCode();
} catch (error) {
  throw new Error('Failed to process data', {
    cause: error,
  });
}
```

`cause` помогает не потерять исходную ошибку.

## Мини-шпаргалка

```javascript
try {
  riskyCode();
} catch (error) {
  // если здесь throw, ошибка пойдет выше
  throw error;
}
```
