# Что делает правило @font-face?

> [!NOTE]
> `@font-face` подключает пользовательский шрифт к странице: задает имя семейства, путь к файлу, формат, начертание, вес и стратегию отображения.

## Главное

```css
@font-face {
  font-family: "Inter";
  src: url("/fonts/inter-regular.woff2") format("woff2");
  font-weight: 400;
  font-style: normal;
  font-display: swap;
}
```

После этого шрифт можно использовать в `font-family`.

```css
body {
  font-family: "Inter", Arial, sans-serif;
}
```

## Несколько начертаний

Для разных весов обычно объявляют отдельные `@font-face`.

```css
@font-face {
  font-family: "Inter";
  src: url("/fonts/inter-bold.woff2") format("woff2");
  font-weight: 700;
  font-style: normal;
  font-display: swap;
}
```

Так браузер понимает, какой файл использовать для `font-weight: 700`.

## font-display

```css
font-display: swap;
```

`swap` позволяет сначала показать текст fallback-шрифтом, а затем заменить его на webfont после загрузки. Это помогает не оставлять текст невидимым.

## Форматы

В современных проектах чаще используют `woff2`: он хорошо сжимается и подходит для веба.

## Мини-шпаргалка

- `@font-face` подключает webfont.
- `font-family` задает имя шрифта.
- `src` указывает файл.
- `font-weight` и `font-style` описывают начертание.
- `font-display: swap` часто улучшает UX загрузки.
- После подключения нужен fallback stack.
