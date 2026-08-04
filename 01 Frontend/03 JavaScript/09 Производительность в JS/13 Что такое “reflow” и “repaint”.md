# Что такое “reflow” и “repaint”?

> [!NOTE] Коротко
> Reflow пересчитывает геометрию элементов, а repaint заново рисует их внешний вид без изменения layout.

## Вопрос

Чем `reflow` отличается от `repaint`?

## Reflow

Reflow, или layout, - пересчет размеров и положения элементов на странице.

Он возникает, когда меняется то, что влияет на геометрию:

- ширина и высота;
- margin, padding;
- display;
- position;
- содержимое текста;
- добавление или удаление DOM-элементов.

## Repaint

Repaint - перерисовка внешнего вида элемента без пересчета геометрии.

Например:

- `color`;
- `background-color`;
- `visibility`;
- `box-shadow`.

## Пример

```javascript
element.style.width = '200px'; // может вызвать reflow
element.style.color = 'red';   // обычно repaint
```

Reflow обычно дороже, потому что может затронуть соседние элементы и всю страницу.

## Layout thrashing

```javascript
items.forEach((item) => {
  item.style.width = `${container.offsetWidth}px`;
});
```

Если код постоянно чередует чтение layout-свойств и запись стилей, браузер может многократно пересчитывать layout.

## Как уменьшить затраты

- группировать чтения и записи DOM;
- использовать CSS-классы вместо множества inline-изменений;
- менять `transform` и `opacity` для анимаций;
- избегать частого чтения layout-свойств после записи.

## Мини-шпаргалка

```text
reflow = geometry/layout
repaint = pixels/style
```
