# Что делает sessionStorage?

> [!NOTE] Коротко
> `sessionStorage` хранит строковые данные в рамках одной вкладки и очищается при закрытии этой вкладки.

## Вопрос

Чем `sessionStorage` отличается от `localStorage`?

## Определение

`sessionStorage` - браузерное хранилище ключ-значение. Данные живут только в пределах текущей вкладки или окна. После закрытия вкладки они удаляются.

Как и `localStorage`, `sessionStorage` хранит только строки и привязан к origin.

## Запись и чтение

```javascript
sessionStorage.setItem('step', '2');

const step = sessionStorage.getItem('step');

console.log(step); // '2'
```

## Удаление

```javascript
sessionStorage.removeItem('step');
sessionStorage.clear();
```

## Объекты

```javascript
const filters = { category: 'books', sort: 'price' };

sessionStorage.setItem('filters', JSON.stringify(filters));

const savedFilters = JSON.parse(sessionStorage.getItem('filters'));
```

## Когда использовать

- временное состояние формы;
- шаг мастера или анкеты;
- данные, которые не должны переживать закрытие вкладки;
- временные UI-настройки.

## Важные ограничения

- данные доступны только в текущей вкладке;
- API синхронный;
- нельзя хранить чувствительные данные без оценки рисков;
- значения всегда строки.

## Мини-шпаргалка

```javascript
sessionStorage.setItem(key, value);
sessionStorage.getItem(key);
sessionStorage.removeItem(key);
sessionStorage.clear();
```
