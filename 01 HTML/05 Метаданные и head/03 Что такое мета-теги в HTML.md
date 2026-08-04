# Что такое мета-теги в HTML?

> [!NOTE]
> Мета-теги - это элементы `<meta>` внутри `<head>`, которые описывают служебную информацию о документе: кодировку, viewport, описание страницы, инструкции для поисковых роботов и данные для социальных сетей.

## Главное

`<meta>` не показывает видимый контент на странице. Он сообщает браузеру и внешним системам, как обрабатывать документ.

```html
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Краткое описание страницы">
</head>
```

## Основные виды meta

| Meta | Назначение |
| --- | --- |
| `charset` | Кодировка документа |
| `viewport` | Настройки viewport на мобильных устройствах |
| `description` | Краткое описание страницы |
| `robots` | Инструкции для поисковых роботов |
| Open Graph | Данные для красивого шаринга в соцсетях |
| `theme-color` | Цвет интерфейса браузера на некоторых устройствах |

## Charset

```html
<meta charset="UTF-8">
```

Помогает браузеру правильно интерпретировать символы.

## Viewport

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

Нужен для нормальной адаптивной верстки на мобильных устройствах.

## Description

```html
<meta
  name="description"
  content="Практический конспект по HTML для frontend-разработчика."
>
```

Описание может использоваться поисковыми системами как сниппет.

## Open Graph

```html
<meta property="og:title" content="Frontend заметки">
<meta property="og:description" content="Конспект по HTML, CSS и JavaScript">
<meta property="og:image" content="https://example.com/cover.png">
```

Эти теги помогают управлять тем, как ссылка выглядит при отправке в мессенджерах и соцсетях.

## Мини-шпаргалка

- `<meta>` живет в `head`.
- Meta-теги не отображаются как контент страницы.
- `charset` отвечает за кодировку.
- `viewport` нужен для адаптивности.
- `description` помогает описать страницу.
- `robots` задает инструкции поисковым роботам.
- Open Graph улучшает вид ссылок при шаринге.
