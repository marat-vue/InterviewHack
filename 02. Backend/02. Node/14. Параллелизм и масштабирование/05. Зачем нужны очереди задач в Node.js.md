# Зачем нужны очереди задач в Node.js?

> [!NOTE]
> Очередь задач позволяет вынести долгую или нестабильную работу из HTTP-запроса в фонового worker-а. Это повышает надежность, снижает latency API и помогает контролировать retries.

## Проблема

Плохой вариант:

```js
app.post('/reports', async (req, res) => {
  const report = await generateHugeReport(req.body);
  res.json(report);
});
```

Клиент ждет долго, запрос может оборваться, а сервер занят тяжелой задачей.

## С очередью

```txt
HTTP API -> queue -> background worker -> result storage
```

API быстро принимает задачу:

```js
app.post('/reports', async (req, res) => {
  const jobId = await queue.add('report', req.body);
  res.status(202).json({ jobId });
});
```

Worker выполняет ее отдельно.

## Что дают очереди?

- retries;
- delayed jobs;
- rate limiting;
- приоритеты;
- обработку всплесков нагрузки;
- отделение API от фоновой работы.

## Примеры задач

- отправка email;
- генерация PDF;
- обработка видео;
- пересчет статистики;
- импорт CSV;
- синхронизация с внешним API.

## Мини-шпаргалка

- Долгую работу не стоит держать внутри HTTP-запроса.
- Очередь возвращает клиенту `202 Accepted` и `jobId`.
- Worker обрабатывает задачи независимо от API.
- Нужны retries и idempotency.
- Популярные инструменты: BullMQ, RabbitMQ, Kafka, cloud queues.
