# Что такое dynamic module?

> [!NOTE]
> Dynamic module - module, который возвращает конфигурацию через статический метод вроде `forRoot`, `register` или `forFeature`. Он нужен, когда module должен настраиваться параметрами.

## Пример идеи

```ts
@Module({})
export class LoggerModule {
  static forRoot(options: LoggerOptions): DynamicModule {
    return {
      module: LoggerModule,
      providers: [
        {
          provide: 'LOGGER_OPTIONS',
          useValue: options,
        },
      ],
      exports: ['LOGGER_OPTIONS'],
    };
  }
}
```

Использование:

```ts
@Module({
  imports: [LoggerModule.forRoot({ level: 'debug' })],
})
export class AppModule {}
```

## forRoot и forFeature

| Метод | Типичный смысл |
|---|---|
| `forRoot` | глобальная настройка module |
| `forFeature` | настройка для конкретной feature |
| `register` | общий стиль регистрации |
| `forRootAsync` | настройка через async factory и DI |

## Мини-шпаргалка

- Dynamic module возвращает `DynamicModule`.
- Используется для configurable modules.
- `forRoot` - настройка верхнего уровня.
- `forFeature` - настройка feature-среза.
- Async-варианты позволяют inject config.
