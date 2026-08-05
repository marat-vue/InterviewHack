# Чем send отличается от emit в ClientProxy?

> [!NOTE]
> `send()` используется для request-response общения и возвращает Observable с ответом. `emit()` отправляет событие без ожидания ответа и тоже возвращает Observable, подтверждающий отправку.

## send

```ts
const result$ = this.client.send<number>(
  { cmd: 'sum' },
  [1, 2, 3],
);
```

На стороне microservice:

```ts
@MessagePattern({ cmd: 'sum' })
sum(data: number[]) {
  return data.reduce((a, b) => a + b, 0);
}
```

## emit

```ts
this.client.emit('user.created', {
  userId: 1,
});
```

На стороне consumer:

```ts
@EventPattern('user.created')
handleUserCreated(event: UserCreatedEvent) {}
```

## Когда что выбирать?

| Метод | Когда |
|---|---|
| `send` | нужен ответ |
| `emit` | событие, fire-and-forget |

## Мини-шпаргалка

- `send` - request-response.
- `emit` - event.
- Оба возвращают cold Observable.
- Для `send` обязательно думай про timeout.
- Event handlers должны быть идемпотентными.
