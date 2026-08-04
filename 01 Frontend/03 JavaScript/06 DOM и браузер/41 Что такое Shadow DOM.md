# Что такое Shadow DOM?

> [!NOTE] Коротко
> Shadow DOM - изолированное DOM-дерево внутри элемента-хоста, которое помогает инкапсулировать разметку и стили компонента.

## Вопрос

Зачем нужен Shadow DOM?

## Определение

Shadow DOM позволяет прикрепить к обычному DOM-элементу отдельное "теневое" дерево. Внутренняя разметка и стили такого дерева изолированы от внешней страницы.

Это важная часть Web Components.

## Создание Shadow DOM

```javascript
const host = document.querySelector('#widget');
const shadowRoot = host.attachShadow({ mode: 'open' });

shadowRoot.innerHTML = `
  <style>
    button {
      color: tomato;
    }
  </style>
  <button>Click</button>
`;
```

Стили внутри Shadow DOM не окрасят все кнопки на странице, а только кнопку внутри этого shadow root.

## Host и shadowRoot

```javascript
console.log(host.shadowRoot); // ShadowRoot, если mode: 'open'
```

Если создать `{ mode: 'closed' }`, доступ к `host.shadowRoot` снаружи будет закрыт.

## Что дает изоляция

- стили компонента не протекают наружу;
- внешние стили меньше влияют на внутренности компонента;
- можно создавать независимые виджеты;
- легче избегать конфликтов CSS-классов.

## Важный нюанс

Shadow DOM не является механизмом безопасности. Это инкапсуляция для структуры и стилей, а не защита секретных данных.

## Мини-шпаргалка

```javascript
const shadow = element.attachShadow({ mode: 'open' });
shadow.innerHTML = '<button>Inside</button>';
```
