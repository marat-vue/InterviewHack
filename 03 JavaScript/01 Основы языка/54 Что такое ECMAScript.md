# ECMAScript

> [!NOTE] Коротко
> ECMAScript - это стандарт языка, а JavaScript - самая известная реализация этого стандарта. Спецификация описывает синтаксис и поведение ядра языка.

## Вопрос

Что такое ECMAScript и чем он отличается от JavaScript?

## Основная идея

ECMAScript - стандарт ECMA-262. Он описывает, как должны работать:

- типы данных;
- операторы;
- функции;
- объекты;
- прототипы;
- промисы;
- модули;
- синтаксис языка.

JavaScript - язык, который реализует этот стандарт в реальных движках.

## Наглядная разница

| ECMAScript | JavaScript |
| --- | --- |
| спецификация | реализация в движках |
| описывает правила языка | используется разработчиками |
| ECMA-262 | V8, SpiderMonkey, JavaScriptCore |
| не включает DOM | в браузере часто используется вместе с DOM |

## Что не является ECMAScript

DOM API не является частью ECMAScript.

```javascript
document.querySelector("button");
```

`document`, `window`, `localStorage`, `fetch` - это Web API браузера, а не ядро ECMAScript.

В Node.js есть свои API:

```javascript
process;
Buffer;
fs;
```

Они тоже не являются частью ECMAScript.

## Версии ECMAScript

Часто говорят ES5, ES6, ES2015, ES2020 и так далее.

ES6 и ES2015 - одно и то же название версии.

```javascript
const name = "Anna";
const message = `Hello, ${name}`;
```

`const` и template literals появились в ES2015.

## Почему это важно

Когда говорят "эта возможность есть в JavaScript", нужно понимать:

- она может быть частью ECMAScript;
- может быть браузерным API;
- может быть API Node.js;
- может требовать транспиляции или полифилла для старых окружений.

## Мини-шпаргалка

| Термин | Значение |
| --- | --- |
| ECMAScript | стандарт языка |
| JavaScript | реализация/используемый язык |
| ECMA-262 | документ спецификации |
| V8 | движок Chrome/Node.js |
| DOM | браузерное API, не ECMAScript |
| ES2015 | то же, что ES6 |
