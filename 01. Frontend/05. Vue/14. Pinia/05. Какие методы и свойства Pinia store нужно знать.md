# Какие методы и свойства Pinia store нужно знать?

> [!NOTE]
> У Pinia store есть полезные служебные методы: `$patch`, `$reset`, `$subscribe`, `$onAction`, `$state`, `$id`, а для компонентов особенно важен `storeToRefs`.

## storeToRefs

Store является reactive object. Если его просто destructure-ить, можно потерять реактивность:

```typescript
const store = useCounterStore();
const { count } = store;
```

Правильно:

```typescript
import { storeToRefs } from "pinia";

const store = useCounterStore();
const { count, doubled } = storeToRefs(store);
const { increment } = store;
```

Actions можно destructure-ить напрямую, потому что они привязаны к store.

## $patch

```typescript
store.$patch({
  count: store.count + 1,
  name: "Anna",
});
```

Для сложных изменений:

```typescript
store.$patch((state) => {
  state.items.push(newItem);
  state.updatedAt = Date.now();
});
```

`$patch` удобно использовать, когда нужно сгруппировать несколько изменений в одно логическое действие.

## $reset

```typescript
store.$reset();
```

В option store `$reset` возвращает state к начальному значению из `state()`. В setup store reset нужно написать самостоятельно.

## $subscribe

```typescript
store.$subscribe((mutation, state) => {
  console.log(mutation.type);
  console.log(state);
});
```

`$subscribe` реагирует на изменения state. Его можно использовать для логов, persistence или аналитики, но не стоит превращать подписки в скрытую бизнес-логику.

## $onAction

```typescript
store.$onAction(({ name, args, after, onError }) => {
  console.log("action started", name, args);

  after((result) => {
    console.log("action finished", result);
  });

  onError((error) => {
    console.error("action failed", error);
  });
});
```

`$onAction` полезен для debugging, metrics и plugins.

## $id и $state

```typescript
store.$id;
store.$state;
```

`$id` - id store. `$state` - текущее state-дерево. Обычно в компонентном коде лучше работать с обычными properties, а не дергать `$state` без необходимости.

## Мини-шпаргалка

- `storeToRefs` сохраняет реактивность при destructuring.
- `$patch` группирует изменения state.
- `$reset` сбрасывает option store.
- `$subscribe` подписывается на state changes.
- `$onAction` подписывается на actions.
- `$id` и `$state` полезны для plugins/debugging.
