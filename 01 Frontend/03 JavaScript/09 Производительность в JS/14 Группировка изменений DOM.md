# Группировка изменений DOM

> [!NOTE]
> DOM-изменения стоит группировать, чтобы уменьшить количество reflow/repaint и не дергать layout без необходимости.

## Вопрос

Как группировать изменения DOM, чтобы повысить производительность?

## Основная идея

Каждое изменение DOM может привести к пересчету layout или перерисовке. Если менять DOM много раз подряд, особенно внутри цикла, браузер может выполнять лишнюю работу.

Лучше подготовить изменения отдельно и применить их одной операцией.

## Плохо: много вставок

```javascript
items.forEach((item) => {
  const li = document.createElement('li');
  li.textContent = item;
  list.append(li);
});
```

Для небольших списков это нормально, но на больших объемах лучше группировать.

## Лучше: DocumentFragment

```javascript
const fragment = document.createDocumentFragment();

items.forEach((item) => {
  const li = document.createElement('li');
  li.textContent = item;
  fragment.append(li);
});

list.append(fragment);
```

В DOM вставляется один подготовленный фрагмент.

## Шаблонная строка

```javascript
list.innerHTML = items
  .map((item) => `<li>${item}</li>`)
  .join('');
```

Так можно быстро вставить известную безопасную разметку. Но нельзя подставлять непроверенный пользовательский HTML.

## Группировка чтений и записей

```javascript
const width = container.offsetWidth;

items.forEach((item) => {
  item.style.width = `${width}px`;
});
```

Сначала читаем layout, потом записываем стили.

## Мини-шпаргалка

```javascript
const fragment = document.createDocumentFragment();
fragment.append(child);
parent.append(fragment);
```
