# Scope chain (цепочка областей видимости)

> [!NOTE] Коротко
> Scope chain - цепочка областей видимости, по которой JavaScript ищет переменные.

## Вопрос

Что такое scope chain?

## Определение

Когда код обращается к переменной, JavaScript сначала ищет ее в текущей области видимости. Если не находит, поднимается во внешнюю область, затем еще выше, пока не дойдет до глобальной области.

Эта последовательность поиска называется scope chain.

## Пример

```javascript
const globalName = 'global';

function outer() {
  const outerName = 'outer';

  function inner() {
    const innerName = 'inner';

    console.log(innerName);
    console.log(outerName);
    console.log(globalName);
  }

  inner();
}

outer();
```

`inner` видит свои переменные, переменные `outer` и глобальные переменные.

## Порядок поиска

```text
inner scope -> outer scope -> global scope
```

Если переменная не найдена нигде, возникнет `ReferenceError`.

## Почему это важно

- объясняет работу замыканий;
- помогает понять лексическую область видимости;
- влияет на доступность переменных;
- помогает читать вложенные функции.

## Мини-шпаргалка

```javascript
function outer() {
  const value = 1;

  function inner() {
    console.log(value); // поиск во внешнем scope
  }
}
```
