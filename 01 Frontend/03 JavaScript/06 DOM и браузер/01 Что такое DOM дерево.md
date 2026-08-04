# Что такое DOM дерево?

> [!NOTE] Коротко
> DOM-дерево - объектное представление HTML-документа, с которым JavaScript может работать как со структурой узлов.

## Вопрос

Что такое DOM и почему его называют деревом?

## Определение

DOM, Document Object Model, - программная модель страницы. Браузер читает HTML и строит из него дерево объектов: документ, элементы, текстовые узлы, комментарии.

JavaScript работает не с исходной HTML-строкой напрямую, а с DOM-узлами.

## Пример HTML

```html
<body>
  <main>
    <h1>Hello</h1>
    <p>Text</p>
  </main>
</body>
```

## Как это выглядит как дерево

```text
document
└─ html
   └─ body
      └─ main
         ├─ h1
         │  └─ "Hello"
         └─ p
            └─ "Text"
```

Каждый элемент становится узлом дерева.

## Что можно делать через DOM

```javascript
const title = document.querySelector('h1');

title.textContent = 'Привет';
title.classList.add('title');
```

Через DOM можно находить элементы, менять текст, атрибуты, классы, стили, создавать и удалять узлы.

## Важные термины

| Термин | Значение |
| --- | --- |
| Node | любой узел DOM |
| Element | HTML-элемент |
| Text node | текст внутри элемента |
| Parent | родительский узел |
| Child | дочерний узел |

## Мини-шпаргалка

```javascript
document.querySelector('button');
element.textContent = 'Save';
element.append(child);
element.remove();
```
