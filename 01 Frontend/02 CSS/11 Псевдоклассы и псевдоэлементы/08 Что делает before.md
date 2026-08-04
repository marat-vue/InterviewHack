# Что делает before?

> [!NOTE]
> `::before` - это CSS-псевдоэлемент, который создает виртуальный контент перед содержимым выбранного элемента. Его часто используют для декоративных элементов, иконок, маркеров и визуальных акцентов.

## Главное

```css
.label::before {
  content: "";
  display: inline-block;
  width: 8px;
  height: 8px;
  margin-right: 8px;
  border-radius: 50%;
  background: #22c55e;
}
```

`::before` появляется внутри элемента перед его реальным содержимым.

## Нужен content

Для `::before` почти всегда нужно указать `content`.

```css
.required::before {
  content: "*";
  color: #b91c1c;
}
```

Если `content` отсутствует, псевдоэлемент обычно не создается.

## Декоративный пример

```css
.quote {
  position: relative;
  padding-left: 24px;
}

.quote::before {
  content: "";
  position: absolute;
  inset-block: 0;
  inset-inline-start: 0;
  width: 4px;
  background: #2563eb;
}
```

Так можно добавить декоративную линию слева от цитаты без лишнего HTML.

## Accessibility-нюанс

Не стоит помещать важный смысловой текст только в `content`. Он может быть недоступен или неудобен для assistive technologies, копирования и перевода.

```css
/* плохо, если это важная информация */
.error::before {
  content: "Ошибка: ";
}
```

Важный текст лучше писать в HTML.

## Мини-шпаргалка

- `::before` создает виртуальный контент перед содержимым.
- Обычно требует `content`.
- Хорош для декора и UI-акцентов.
- Может быть inline, block или absolute.
- Важный смысловой текст лучше держать в HTML.
