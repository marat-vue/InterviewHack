# Как настроить тему Vuetify?

> [!NOTE]
> Vuetify theme задает colors, dark/light mode и default theme приложения. Тему настраивают в `createVuetify`, а затем используют через component props, CSS variables и theme composables.

## Базовая тема

```typescript
import { createVuetify } from "vuetify";

export const vuetify = createVuetify({
  theme: {
    defaultTheme: "light",
    themes: {
      light: {
        dark: false,
        colors: {
          primary: "#2563eb",
          secondary: "#64748b",
          error: "#dc2626",
        },
      },
    },
  },
});
```

Теперь можно использовать:

```vue
<v-btn color="primary">Сохранить</v-btn>
<v-alert color="error">Ошибка</v-alert>
```

## Dark theme

```typescript
themes: {
  light: { dark: false },
  dark: { dark: true },
}
```

Переключение темы можно сделать через Vuetify theme composable:

```typescript
import { useTheme } from "vuetify";

const theme = useTheme();

function toggleTheme() {
  theme.global.name.value =
    theme.global.current.value.dark ? "light" : "dark";
}
```

## Defaults

Vuetify позволяет задать defaults для компонентов:

```typescript
createVuetify({
  defaults: {
    VBtn: {
      rounded: "lg",
      variant: "flat",
    },
    VTextField: {
      variant: "outlined",
      density: "comfortable",
    },
  },
});
```

Это помогает держать UI консистентным.

## Мини-шпаргалка

- Theme настраивают в `createVuetify`.
- `defaultTheme` выбирает стартовую тему.
- `colors.primary` потом используется как `color="primary"`.
- `useTheme` позволяет переключать тему в runtime.
- `defaults` задают стандартные props компонентов.
