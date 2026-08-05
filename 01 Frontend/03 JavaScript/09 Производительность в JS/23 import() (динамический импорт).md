# import() (динамический импорт)

> [!NOTE]
> `import()` загружает модуль динамически во время выполнения и возвращает Promise.

## Вопрос

Что делает динамический импорт `import()`?

## Определение

`import('./module.js')` - функция-подобный синтаксис, который асинхронно загружает модуль. В отличие от статического `import`, его можно вызывать по условию, внутри функции или обработчика события.

## Пример

```javascript
button.addEventListener('click', async () => {
  const module = await import('./dialog.js');

  module.openDialog();
});
```

Модуль `dialog.js` загрузится только после клика.

## Деструктуризация экспорта

```javascript
const { formatDate } = await import('./date-utils.js');

console.log(formatDate(new Date()));
```

## Обработка ошибок

```javascript
try {
  const module = await import('./feature.js');
  module.run();
} catch (error) {
  console.error('Failed to load module', error);
}
```

Загрузка может упасть из-за сети, неправильного пути или ошибки в модуле.

## Где полезен

- code splitting;
- lazy loading тяжелых библиотек;
- загрузка редких функций;
- условные polyfills;
- роутинг в SPA.

## Мини-шпаргалка

```javascript
const module = await import('./module.js');
module.someExport();
```
