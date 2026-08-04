# Надстройка над JavaScript

> [!NOTE] Коротко
> TypeScript является надстройкой над JavaScript: он добавляет типы и инструменты проверки, но исполняется как JavaScript после компиляции.

## Вопрос

Почему TypeScript называют надстройкой над JavaScript?

## Определение

TypeScript не является отдельной платформой выполнения. Он расширяет синтаксис JavaScript типами, интерфейсами, generics, utility types и другими возможностями для разработки.

После компиляции TypeScript превращается в JavaScript, который запускается в браузере, Node.js или другом JS-окружении.

## Пример

```typescript
type User = {
  id: number;
  name: string;
};

const user: User = {
  id: 1,
  name: 'Ann',
};
```

Тип `User` помогает разработчику и компилятору, но в итоговом JavaScript его не будет.

## Что остается после компиляции

```javascript
const user = {
  id: 1,
  name: 'Ann',
};
```

Типы удаляются, потому что JavaScript-движок не понимает TypeScript-аннотации.

## Почему это важно

- TS не исправляет runtime-ошибки автоматически;
- проверки типов работают до запуска;
- внешние данные все равно нужно валидировать;
- знание JavaScript остается обязательным.

## Простой вывод

TypeScript помогает писать JavaScript безопаснее, но не отменяет правила JavaScript: области видимости, прототипы, Event Loop, замыкания, `this`.

## Мини-шпаргалка

```text
write TypeScript -> check types -> emit JavaScript -> run JavaScript
```
