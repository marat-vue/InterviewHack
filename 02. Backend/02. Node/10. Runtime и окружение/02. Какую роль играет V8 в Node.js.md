# Какую роль играет V8 в Node.js?

> [!NOTE]
> V8 - JavaScript-движок, который парсит, компилирует и выполняет JavaScript-код внутри Node.js. Он отвечает за выполнение JS, оптимизации, garbage collection и работу с памятью JavaScript heap.

## Что делает V8?

V8 берет исходный JavaScript-код и превращает его в исполняемые инструкции.

```txt
JavaScript source -> parser -> bytecode -> optimized machine code
```

В реальности процесс сложнее, но для понимания Node.js важно знать: V8 исполняет JS, а Node.js добавляет системные возможности вокруг него.

## V8 не делает все

V8 не умеет сам читать файл или слушать TCP-порт. Для этого Node.js связывает JS-код с C/C++-частью, libuv и API операционной системы.

```js
import { readFile } from 'node:fs/promises';

await readFile('file.txt', 'utf8');
```

В этом примере JavaScript-часть выполняется V8, а реальное обращение к файловой системе проходит через Node.js/libuv/ОС.

## V8 и память

Объекты JavaScript живут в heap, которым управляет V8. Если объект больше недостижим, garbage collector может освободить память.

```js
let users = [{ id: 1 }];
users = null; // старый массив больше не нужен, GC сможет его убрать позже
```

Важно: `Buffer` и некоторые native-ресурсы могут занимать память вне обычной JS heap.

## Мини-шпаргалка

- V8 выполняет JavaScript.
- V8 управляет JS heap и garbage collection.
- Node.js добавляет к V8 доступ к ОС.
- Оптимизации V8 зависят от формы кода и типов данных.
- Не вся память Node.js видна только как `heapUsed`.
