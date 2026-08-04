# Как работает механизм SPA-навигации?

> [!NOTE] Коротко
> SPA-навигация меняет URL через History API и заменяет компонент в `RouterView`, не загружая HTML-страницу с сервера заново.

## Вопрос

Как работает механизм SPA-навигации?

## Обычная навигация

При переходе по классической ссылке браузер запрашивает новый HTML-документ у сервера.

```html
<a href="/profile">Профиль</a>
```

## SPA-навигация

Vue Router перехватывает переход, меняет адрес и рендерит нужный компонент.

```vue
<RouterLink to="/profile">Профиль</RouterLink>
<RouterView />
```

Страница не перезагружается полностью, меняется только интерфейс внутри приложения.

## History mode

```typescript
const router = createRouter({
  history: createWebHistory(),
  routes,
});
```

`createWebHistory` использует History API и красивые URL без `#`.

## Hash mode

```typescript
const router = createRouter({
  history: createWebHashHistory(),
  routes,
});
```

Hash mode хранит маршрут после `#` и проще работает на статическом хостинге без настройки fallback.

## Мини-шпаргалка

- SPA не перезагружает HTML-документ при переходе.
- Router меняет URL и компонент в `RouterView`.
- `createWebHistory` требует server fallback на `index.html`.
- `createWebHashHistory` проще для статического деплоя.
