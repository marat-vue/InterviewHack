# Как тестировать controller в NestJS?

> [!NOTE]
> Controller можно тестировать как обычный class с mocked service или через TestingModule. Обычно в unit-тесте controller проверяют, что он правильно передает DTO/params в service и возвращает результат.

## Пример

```ts
describe('UsersController', () => {
  let controller: UsersController;
  const usersService = {
    findAll: jest.fn().mockResolvedValue([]),
  };

  beforeEach(async () => {
    const moduleRef = await Test.createTestingModule({
      controllers: [UsersController],
      providers: [{ provide: UsersService, useValue: usersService }],
    }).compile();

    controller = moduleRef.get(UsersController);
  });

  it('returns users', async () => {
    await expect(controller.findAll()).resolves.toEqual([]);
  });
});
```

## Что не проверять в unit controller test?

- реальные HTTP requests;
- validation pipe;
- guards;
- serialization;
- database.

Для этого лучше e2e tests.

## Мини-шпаргалка

- Controller unit test проверяет controller logic.
- Service обычно mock.
- HTTP lifecycle лучше проверять e2e.
- Тонкие controllers тестируются легко.
- Если controller содержит много логики, ее лучше вынести в service.
