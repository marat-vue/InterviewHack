# Как работать с транзакциями в NestJS?

> [!NOTE]
> Транзакции в NestJS зависят от выбранного ORM или database driver. Важно держать транзакционную границу на уровне use case и не смешивать ее с controller-логикой.

## Prisma пример

```ts
await this.prisma.$transaction(async (tx) => {
  const order = await tx.order.create({ data: orderData });

  await tx.orderItem.createMany({
    data: items.map((item) => ({ ...item, orderId: order.id })),
  });

  return order;
});
```

## Где начинать транзакцию?

Обычно в service/use case:

```txt
Controller -> OrdersService.createOrder -> transaction
```

Controller не должен управлять database transaction напрямую.

## Осторожно

Не делай внутри транзакции долгие внешние HTTP-запросы. Это держит locks и connections дольше нужного.

## Мини-шпаргалка

- Транзакции зависят от ORM/driver.
- Граница транзакции должна быть вокруг use case.
- Controller не должен знать про transaction details.
- Не держи транзакцию открытой во время внешних API calls.
- Для конфликтов нужен retry/idempotency.
