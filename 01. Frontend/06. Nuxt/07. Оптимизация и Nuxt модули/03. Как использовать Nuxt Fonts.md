# Как использовать Nuxt Fonts?

> [!NOTE]
> Nuxt Fonts автоматически оптимизирует web fonts, анализируя CSS `font-family`, находя local/provider fonts, генерируя `@font-face` и уменьшая ручную работу с preload/preconnect/self-hosting.

## Установка

```bash
npx nuxi@latest module add fonts
```

Вручную:

```ts
export default defineNuxtConfig({
  modules: ['@nuxt/fonts'],
});
```

## Использование через CSS

```css
/* app/assets/css/main.css */
body {
  font-family: 'Inter', sans-serif;
}
```

Nuxt Fonts анализирует CSS и генерирует нужные font declarations.

## Настройка

```ts
export default defineNuxtConfig({
  fonts: {
    defaults: {
      weights: [400, 500, 700],
      styles: ['normal'],
      subsets: ['latin', 'cyrillic'],
    },
  },
});
```

## Providers

Nuxt Fonts может искать fonts:

- locally в `public/`;
- через Google;
- Bunny;
- Fontshare;
- другие providers.

Смысл: использовать лучший доступный источник и оптимизировать output.

## Performance советы

- не подключай 10 начертаний без необходимости;
- выбирай нужные subsets;
- используй `woff2`;
- избегай layout shift из-за шрифтов;
- проверяй итоговый CSS и network.

## Мини-шпаргалка

- Nuxt Fonts обрабатывает `font-family` в CSS.
- Inline `font-family` в template не подходит для анализа.
- По умолчанию модуль оптимизирует загрузку.
- Настраивай weights/styles/subsets.
- Шрифты сильно влияют на CLS и LCP.
