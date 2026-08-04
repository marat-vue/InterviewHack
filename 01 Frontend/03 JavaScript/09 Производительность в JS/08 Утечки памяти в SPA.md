# Утечки памяти в SPA

> [!NOTE] Коротко
> В SPA утечки особенно опасны, потому что страница живет долго, а компоненты постоянно создаются и удаляются без полной перезагрузки.

## Вопрос

Почему memory leaks особенно заметны в Single Page Applications?

## Определение

SPA не перезагружает страницу при переходах между экранами. Поэтому память не очищается автоматически полной перезагрузкой документа. Если компоненты оставляют после себя слушатели, таймеры или подписки, приложение постепенно тяжелеет.

## Частый пример: забытый listener

```javascript
function mountComponent() {
  window.addEventListener('resize', handleResize);
}

function unmountComponent() {
  window.removeEventListener('resize', handleResize);
}
```

Если не вызвать `removeEventListener`, обработчик останется жить после удаления компонента.

## Таймеры

```javascript
const id = setInterval(update, 1000);

function cleanup() {
  clearInterval(id);
}
```

Интервалы обязательно нужно очищать.

## Подписки

```javascript
const unsubscribe = store.subscribe(render);

function cleanup() {
  unsubscribe();
}
```

Любая подписка должна иметь понятный момент отписки.

## Типичные источники утечек в SPA

- event listeners на `window` и `document`;
- `setInterval`;
- WebSocket-подписки;
- observers;
- большие кэши;
- ссылки на удаленные DOM-элементы;
- незавершенные async-операции.

## Мини-шпаргалка

```javascript
mount -> subscribe/listen/start
unmount -> unsubscribe/remove/clear/abort
```
