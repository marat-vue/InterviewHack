# Что такое Open Graph?

> [!NOTE]
> **Open Graph** - это набор мета-тегов, которые описывают, как ссылка на страницу должна выглядеть при публикации в социальных сетях, мессенджерах и других сервисах предпросмотра.

## Главное

Open Graph помогает управлять карточкой ссылки: заголовком, описанием, изображением и типом страницы.

```html
<meta property="og:title" content="Frontend заметки">
<meta property="og:description" content="Конспект по HTML, CSS и JavaScript">
<meta property="og:image" content="https://example.com/cover.jpg">
<meta property="og:url" content="https://example.com/html">
<meta property="og:type" content="article">
```

Без этих тегов сервис сам попытается выбрать заголовок, описание и картинку, но результат может быть неудачным.

## Основные og-теги

| Тег | Что задает |
| --- | --- |
| `og:title` | Заголовок карточки |
| `og:description` | Краткое описание |
| `og:image` | Картинку предпросмотра |
| `og:url` | Канонический URL страницы |
| `og:type` | Тип объекта: `website`, `article`, `product` |
| `og:site_name` | Название сайта |

## Пример для статьи

```html
<head>
  <title>Семантика HTML - Frontend Notes</title>
  <meta name="description" content="Разбор семантической HTML-разметки">

  <meta property="og:type" content="article">
  <meta property="og:title" content="Семантика HTML">
  <meta property="og:description" content="Как выбирать HTML-теги по смыслу">
  <meta property="og:image" content="https://example.com/og/html-semantics.png">
  <meta property="og:url" content="https://example.com/html/semantics">
</head>
```

## Open Graph и SEO

Open Graph не заменяет обычные SEO-теги вроде `title` и `description`. Он больше влияет на вид ссылки при шаринге, а не напрямую на ранжирование.

## Мини-шпаргалка

- Open Graph управляет карточкой ссылки.
- OG-теги размещаются в `head`.
- Используют атрибут `property`, а не `name`.
- Самые важные: `og:title`, `og:description`, `og:image`, `og:url`.
- Для красивого шаринга нужна абсолютная ссылка на изображение.
