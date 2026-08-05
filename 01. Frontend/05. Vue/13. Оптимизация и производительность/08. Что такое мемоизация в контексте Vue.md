# Что такое мемоизация в контексте Vue?

> [!NOTE]
> **Мемоизация** - это сохранение результата вычисления, чтобы не выполнять одну и ту же дорогую работу повторно, пока входные данные не изменились.

## Главное

Во Vue мемоизация чаще всего встречается в `computed`. Vue запоминает результат вычисления и пересчитывает его только тогда, когда изменились реактивные зависимости.

```vue
<script setup>
import { computed, ref } from "vue";

const query = ref("");
const users = ref([]);

const filteredUsers = computed(() =>
  users.value.filter((user) =>
    user.name.toLowerCase().includes(query.value.toLowerCase())
  )
);
</script>
```

Если меняется состояние, которое не связано с `query` или `users`, `filteredUsers` не пересчитывается.

## Без мемоизации

Метод вызывается заново при каждом рендере компонента.

```vue
<script setup>
const getFilteredUsers = () =>
  users.value.filter((user) => user.isActive);
</script>

<template>
  <UserList :users="getFilteredUsers()" />
</template>
```

Если фильтрация тяжелая, такой подход может создавать лишнюю нагрузку.

## С мемоизацией через computed

```vue
<script setup>
import { computed } from "vue";

const activeUsers = computed(() =>
  users.value.filter((user) => user.isActive)
);
</script>

<template>
  <UserList :users="activeUsers" />
</template>
```

Теперь результат кешируется до тех пор, пока `users` не изменится.

## Где еще встречается идея мемоизации

- `computed` кеширует производные значения.
- `v-memo` пропускает обновление части шаблона, если зависимости не изменились.
- В composables можно вручную кешировать результаты дорогих операций.
- В store можно хранить уже подготовленные данные, если они нужны многим компонентам.

## Пример ручного кеша

```js
const cache = new Map();

export function getFormatter(locale) {
  if (!cache.has(locale)) {
    cache.set(locale, new Intl.DateTimeFormat(locale));
  }

  return cache.get(locale);
}
```

Такой кеш полезен для объектов, создание которых дорогое и повторяется много раз.

## Когда мемоизация вредна

Мемоизация усложняет код и тоже занимает память. Она не нужна для простых вычислений вроде сложения двух чисел или короткой строки.

```js
const fullName = `${firstName.value} ${lastName.value}`;
```

Если вычисление дешевое, дополнительный кеш может быть лишним.

## Мини-шпаргалка

- Мемоизация хранит результат вычисления.
- Во Vue главный инструмент мемоизации - `computed`.
- Методы в шаблоне вызываются при рендере, `computed` кешируется.
- `v-memo` оптимизирует рендер части шаблона.
- Мемоизацию стоит применять там, где есть реальная цена пересчета.
