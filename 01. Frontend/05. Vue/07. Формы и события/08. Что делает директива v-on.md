# Что делает директива v-on?

> [!NOTE]
> `v-on` подписывает элемент или компонент на событие и вызывает обработчик. Короткая запись - `@`.

## Вопрос

Что делает директива `v-on`?

## Базовый пример

```vue
<script setup>
function submit() {
  console.log("submit");
}
</script>

<template>
  <button v-on:click="submit">Отправить</button>
</template>
```

При клике Vue вызовет `submit`.

## Сокращение

```vue
<button @click="submit">Отправить</button>
```

В реальных проектах чаще используют `@click`.

## С аргументами

```vue
<button @click="selectUser(user.id)">Выбрать</button>
```

Если нужен объект события:

```vue
<input @input="handleInput($event)" />
```

## Модификаторы

```vue
<form @submit.prevent="submit">
  <button>Сохранить</button>
</form>
```

`.prevent` предотвращает стандартное поведение формы.

## События компонентов

```vue
<BaseModal @close="isOpen = false" />
```

Компонент может отправить событие через `emit`, а родитель слушает его через `v-on`.

## Мини-шпаргалка

- `v-on:event="handler"` слушает событие.
- `@event="handler"` - короткая запись.
- `$event` передает объект события.
- Модификаторы управляют поведением события.
- Компонентные события слушаются так же, как DOM-события.
