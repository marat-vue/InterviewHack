# Что такое hydration и hydration mismatch?

> [!NOTE]
> Hydration - процесс, когда Vue на клиенте подключает интерактивность к HTML, который уже пришел с сервера. Hydration mismatch возникает, когда server HTML и первый client render отличаются.

## Как работает hydration?

```text
Server rendered HTML -> browser показывает страницу -> JS загружается -> Vue подключает events/state
```

После hydration кнопки, формы, меню и реактивность начинают работать как обычное Vue-приложение.

## Что такое mismatch?

Server отдал:

```html
<span>100</span>
```

Client при первом render получил:

```html
<span>101</span>
```

Vue видит различие и предупреждает о hydration mismatch.

## Частые причины

- `Math.random()` в template;
- `Date.now()` при SSR;
- разные timezone;
- обращение к `window`;
- browser-only data на сервере;
- разные cookies/server/client state;
- условный render по client-only признаку.

## Плохой пример

```vue
<template>
  <p>{{ Math.random() }}</p>
</template>
```

Server и client почти точно получат разные числа.

## Хороший пример

```vue
<script setup lang="ts">
const id = useState('stable-id', () => crypto.randomUUID());
</script>

<template>
  <p>{{ id }}</p>
</template>
```

`useState` передаст значение через payload и сохранит его при hydration.

## Мини-шпаргалка

- Hydration подключает Vue к server HTML.
- Mismatch = server HTML отличается от client render.
- Не используй случайность и текущую дату прямо в template.
- Browser-only код прячь за `import.meta.client`.
- `useState` помогает сохранить SSR-friendly state.

