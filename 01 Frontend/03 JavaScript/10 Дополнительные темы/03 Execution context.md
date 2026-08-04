# Execution context

> [!NOTE] Коротко
> Execution context - окружение, в котором JavaScript выполняет код и хранит информацию о переменных, `this` и области видимости.

## Вопрос

Что такое контекст выполнения в JavaScript?

## Определение

Execution context, или контекст выполнения, - внутренняя структура движка JavaScript для запуска кода. В ней хранится, какие переменные доступны, чему равен `this`, какая цепочка областей видимости используется и где продолжать выполнение.

## Основные виды

| Контекст | Когда создается |
| --- | --- |
| Global Execution Context | при запуске скрипта |
| Function Execution Context | при каждом вызове функции |
| Module Execution Context | при выполнении ES-модуля |
| Eval Execution Context | при выполнении `eval` |

## Пример

```javascript
const globalValue = 1;

function sum(a, b) {
  const result = a + b;
  return result + globalValue;
}

sum(2, 3);
```

При запуске создается глобальный контекст. При вызове `sum` создается новый функциональный контекст.

## Что хранит контекст

- lexical environment;
- variable environment;
- значение `this`;
- ссылку на внешнюю область видимости;
- информацию для выполнения текущего кода.

## Связь со стеком вызовов

Когда функция вызывается, ее execution context помещается в Call Stack. Когда функция завершается, контекст удаляется из стека.

```text
Global context -> function context -> nested function context
```

## Мини-шпаргалка

```text
execution context = variables + scope + this + code position
```
