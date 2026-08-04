# Generic без extends

> [!NOTE] Коротко
> Generic без `extends` не всегда ошибка, но становится антипаттерном, если код внутри требует конкретной формы значения. В таком случае ограничение нужно указать явно.

## Вопрос

Почему generic без `extends` может быть проблемой?

## Нормальный generic без ограничения

Если функция просто сохраняет тип и не обращается к специфичным полям, ограничение не нужно.

```typescript
function identity<T>(value: T): T {
  return value;
}
```

Здесь `T` действительно может быть любым.

## Проблемный пример

```typescript
function getId<T>(value: T): string {
  // return value.id; // ошибка
  return "";
}
```

Код хочет использовать `id`, но generic не сообщает TypeScript, что `id` существует.

## Правильное ограничение

```typescript
function getId<T extends { id: string }>(value: T): string {
  return value.id;
}

getId({ id: "1", name: "Анна" });
// getId({ name: "Анна" }); // ошибка
```

## Ограничение ключами

```typescript
function getProperty<T, K extends keyof T>(object: T, key: K): T[K] {
  return object[key];
}
```

Это лучше, чем принимать произвольную строку в качестве ключа.

## Мини-шпаргалка

- Generic без `extends` нормален, если `T` может быть любым.
- Если нужен доступ к полям, добавляй ограничение.
- `T extends { id: string }` описывает минимальную форму.
- `K extends keyof T` ограничивает ключи объекта.
