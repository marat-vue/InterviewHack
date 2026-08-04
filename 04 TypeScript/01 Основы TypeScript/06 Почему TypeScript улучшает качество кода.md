# Почему TypeScript улучшает качество кода?

> [!NOTE] Коротко
> TypeScript улучшает качество кода за счет явных контрактов, ранних проверок и лучшей поддержки рефакторинга.

## Вопрос

Почему TypeScript часто выбирают для крупных frontend-проектов?

## Контракты между частями кода

Типы описывают, какие данные принимает и возвращает функция.

```typescript
type User = {
  id: number;
  name: string;
};

function renderUser(user: User): string {
  return user.name;
}
```

Сразу видно, что функция ожидает объект пользователя.

## Меньше случайных ошибок

```typescript
function formatPrice(price: number) {
  return price.toFixed(2);
}

formatPrice('100'); // ошибка TypeScript
```

TS не позволит случайно передать строку вместо числа.

## Легче читать чужой код

Типы помогают понять структуру данных без постоянного поиска по проекту.

```typescript
type ApiResponse<T> = {
  data: T;
  error?: string;
};
```

## Безопаснее менять код

При переименовании свойства или изменении сигнатуры функции TypeScript покажет места, которые нужно обновить.

## Командная разработка

В команде типы работают как договор: компонент, функция или модуль явно сообщает, что ему нужно и что он возвращает.

## Мини-шпаргалка

```text
TypeScript improves quality through contracts, checks, navigation and refactoring
```
