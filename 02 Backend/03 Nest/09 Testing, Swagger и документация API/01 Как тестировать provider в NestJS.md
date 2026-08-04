# Как тестировать provider в NestJS?

> [!NOTE]
> Provider в NestJS обычно тестируют через `TestingModule`, который создает небольшой DI-контейнер для теста. Зависимости можно заменить mocks через custom providers.

## Пример

```ts
describe('UsersService', () => {
  let service: UsersService;

  beforeEach(async () => {
    const moduleRef = await Test.createTestingModule({
      providers: [UsersService],
    }).compile();

    service = moduleRef.get(UsersService);
  });

  it('returns users', () => {
    expect(service.findAll()).toEqual([]);
  });
});
```

## С mock dependency

```ts
const usersRepositoryMock = {
  findAll: jest.fn().mockResolvedValue([]),
};

providers: [
  UsersService,
  { provide: UsersRepository, useValue: usersRepositoryMock },
];
```

## Что проверять?

- бизнес-правила;
- ошибки;
- вызовы зависимостей;
- edge cases;
- transaction flow.

## Мини-шпаргалка

- `Test.createTestingModule` создает тестовый module.
- `moduleRef.get` достает provider.
- Dependencies заменяются через `useValue`.
- Unit test не должен поднимать весь сервер.
- Чем меньше service знает про framework, тем проще тест.
