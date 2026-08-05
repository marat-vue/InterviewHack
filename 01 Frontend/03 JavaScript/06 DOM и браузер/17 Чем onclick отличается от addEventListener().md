# Чем onclick отличается от addEventListener()?

> [!NOTE]
> `onclick` - свойство элемента для одного обработчика, а `addEventListener()` позволяет добавлять несколько обработчиков и управлять фазами события.

## Вопрос

Почему обычно лучше использовать `addEventListener()`, а не `onclick`?

## onclick

`onclick` - свойство DOM-элемента. В нем может храниться только одна функция.

```javascript
button.onclick = () => {
  console.log('first');
};

button.onclick = () => {
  console.log('second');
};
```

Второе присваивание перезапишет первое.

## addEventListener()

`addEventListener()` добавляет обработчик, не удаляя уже существующие.

```javascript
button.addEventListener('click', () => {
  console.log('first');
});

button.addEventListener('click', () => {
  console.log('second');
});
```

Оба обработчика выполнятся.

## Сравнение

| Критерий | `onclick` | `addEventListener()` |
| --- | --- | --- |
| Количество обработчиков | один | несколько |
| Перезапись | да | нет |
| Опции `once`, `passive`, `capture` | нет | да |
| Удаление | присвоить `null` | `removeEventListener()` |
| Практика | редко | основной способ |

## Когда onclick допустим

`onclick` можно встретить в простых примерах или быстрых прототипах, но в рабочем коде чаще выбирают `addEventListener()`.

## Мини-шпаргалка

```javascript
button.onclick = handler; // один обработчик
button.addEventListener('click', handler); // гибкая подписка
```
