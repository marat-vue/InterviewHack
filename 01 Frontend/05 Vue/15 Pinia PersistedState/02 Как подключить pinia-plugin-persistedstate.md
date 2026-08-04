# Как подключить pinia-plugin-persistedstate?

> [!NOTE]
> `pinia-plugin-persistedstate` подключается как plugin к Pinia instance через `pinia.use(piniaPluginPersistedstate)`, после чего в stores появляется опция `persist`.

## Установка

```bash
npm install pinia-plugin-persistedstate
```

## Подключение в main.ts

```typescript
import { createApp } from "vue";
import { createPinia } from "pinia";
import piniaPluginPersistedstate from "pinia-plugin-persistedstate";
import App from "./App.vue";

const app = createApp(App);
const pinia = createPinia();

pinia.use(piniaPluginPersistedstate);

app.use(pinia);
app.mount("#app");
```

Порядок важен: сначала создаем Pinia, подключаем plugin к Pinia, потом передаем Pinia в приложение.

## Включение persistence в store

```typescript
export const useSettingsStore = defineStore("settings", {
  state: () => ({
    theme: "light" as "light" | "dark",
    language: "ru",
  }),
  persist: true,
});
```

По умолчанию plugin сохраняет весь state store. Это удобно для маленьких settings stores, но опасно для больших или чувствительных stores.

## Где появятся данные?

По умолчанию обычно используется `localStorage`, а ключ строится на основе id store.

```txt
localStorage:
settings -> {"theme":"dark","language":"ru"}
```

## Мини-шпаргалка

- Установка: `npm install pinia-plugin-persistedstate`.
- Подключение: `pinia.use(piniaPluginPersistedstate)`.
- В store включают `persist: true`.
- По умолчанию сохраняется весь state.
- Для auth и больших stores лучше настраивать `pick`.
