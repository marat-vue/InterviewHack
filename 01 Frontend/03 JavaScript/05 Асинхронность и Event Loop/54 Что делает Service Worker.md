# Что делает Service Worker?

> [!NOTE] Коротко
> Service Worker - фоновый скрипт браузера, который может перехватывать сетевые запросы, кэшировать ресурсы и помогать приложению работать офлайн.

## Вопрос

Зачем нужен Service Worker и чем он отличается от Web Worker?

## Определение

Service Worker - специальный worker, который работает между веб-страницей и сетью. Он может перехватывать `fetch`-запросы, отдавать данные из кэша, получать push-уведомления и выполнять фоновую логику.

Он не имеет доступа к DOM и общается со страницей через сообщения.

## Регистрация

```javascript
if ('serviceWorker' in navigator) {
  navigator.serviceWorker.register('/service-worker.js');
}
```

Обычно Service Worker работает только на HTTPS или на `localhost`.

## service-worker.js

```javascript
self.addEventListener('install', (event) => {
  console.log('Service Worker installed');
});

self.addEventListener('fetch', (event) => {
  event.respondWith(fetch(event.request));
});
```

Событие `fetch` позволяет перехватывать запросы страницы.

## Пример кэширования

```javascript
self.addEventListener('install', (event) => {
  event.waitUntil(
    caches.open('app-v1').then((cache) => {
      return cache.addAll(['/index.html', '/styles.css']);
    })
  );
});
```

`event.waitUntil()` говорит браузеру дождаться промиса перед завершением этапа установки.

## Service Worker vs Web Worker

| Критерий | Web Worker | Service Worker |
| --- | --- | --- |
| Основная задача | вычисления в фоне | сеть, кэш, offline |
| Жизненный цикл | связан со страницей | управляется браузером |
| DOM | нет доступа | нет доступа |
| Сетевые запросы | не перехватывает | может перехватывать |

## Мини-шпаргалка

```javascript
navigator.serviceWorker.register('/service-worker.js');

self.addEventListener('fetch', (event) => {
  event.respondWith(fetch(event.request));
});
```
