# Что такое тип string?

> [!NOTE] Коротко
> `string` описывает строковые значения: обычные строки, шаблонные строки и результат операций со строками.

## Вопрос

Что означает тип `string` в TypeScript?

## Определение

`string` - примитивный тип для текста. Он соответствует строкам JavaScript и используется для имен, сообщений, URL, CSS-классов, ключей и любых текстовых данных.

## Пример

```typescript
let title: string = 'TypeScript';
let message: string = `Hello, ${title}`;
```

## Ошибка типа

```typescript
let name: string = 'Ann';

name = 123; // ошибка TypeScript
```

Переменной типа `string` нельзя присвоить число.

## Методы строк

```typescript
const email: string = ' USER@EXAMPLE.COM ';

const normalized = email.trim().toLowerCase();

console.log(normalized); // 'user@example.com'
```

TypeScript знает методы строк и подсказывает их в редакторе.

## String literal types

```typescript
type Theme = 'light' | 'dark';

let theme: Theme = 'dark';
theme = 'blue'; // ошибка
```

Строковые литеральные типы позволяют ограничить значение конкретными строками.

## string vs String

```typescript
const value: string = 'text'; // правильно
const objectValue: String = new String('text'); // редко нужно
```

В большинстве случаев нужно использовать `string`.

## Мини-шпаргалка

```typescript
let text: string = 'hello';
type Status = 'idle' | 'loading' | 'error';
```
