# Когда использовать any?

> [!NOTE]
> `any` стоит использовать редко и точечно, когда тип временно невозможно или слишком дорого описать безопасно.

## Вопрос

Когда `any` оправдан, а когда это антипаттерн?

## Когда any может быть оправдан

`any` допустим как временный инструмент, если он помогает двигаться дальше, но лучше оставлять его локальным и понятным.

## Миграция JavaScript в TypeScript

```typescript
function legacyAdapter(data: any) {
  return oldLibrary.process(data);
}
```

Иногда проект переводят на TS постепенно, и часть старого кода временно остается через `any`.

## Сторонняя библиотека без типов

```typescript
declare const legacyWidget: any;
```

Если библиотека не имеет нормальных типов, `any` может быть временным мостом.

## Когда лучше не использовать

```typescript
function createUser(payload: any) {
  return payload.name.toUpperCase();
}
```

Для данных API или формы лучше использовать `unknown` и выполнить проверку.

## Как ограничить вред

- держать `any` как можно ближе к границе;
- не передавать `any` глубоко в приложение;
- добавлять комментарий с причиной;
- постепенно заменять на конкретный тип;
- предпочитать `unknown`, если значение нужно проверить.

## Пример безопаснее

```typescript
function parseUser(value: unknown): User {
  if (isUser(value)) {
    return value;
  }

  throw new Error('Invalid user');
}
```

## Мини-шпаргалка

```typescript
// temporary boundary only
const legacyValue: any = getLegacyValue();
```
