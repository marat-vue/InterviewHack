# Как использовать overrideProvider?

> [!NOTE]
> `overrideProvider` позволяет заменить provider в testing module после объявления imports. Это удобно в e2e и integration tests, когда нужно подменить database, external API client или auth service.

## Пример

```ts
const moduleRef = await Test.createTestingModule({
  imports: [AppModule],
})
  .overrideProvider(PaymentClient)
  .useValue(paymentClientMock)
  .compile();
```

## Когда полезно?

- заменить внешний API;
- заменить email sender;
- заменить clock;
- заменить auth client;
- подменить repository;
- изолировать test от реального сервиса.

## overrideGuard

Для guards есть похожий подход.

```ts
.overrideGuard(JwtAuthGuard)
.useValue({ canActivate: () => true })
```

## Мини-шпаргалка

- `overrideProvider` подменяет provider в test module.
- Особенно полезен при imports настоящего module.
- Для guards есть `overrideGuard`.
- Не ходи в реальные внешние API из тестов.
- Mocks должны быть достаточно похожи на реальные контракты.
