# Для чего используется хук beforeCreate?

> [!NOTE]
> `beforeCreate` - ранний хук Options API во Vue 2, который вызывается до инициализации `data`, `computed`, `methods` и watchers. В современном Vue 3 он почти не нужен, потому что его роль обычно закрывает `setup`.

## Вопрос

Для чего используется хук `beforeCreate`?

## Когда вызывается

`beforeCreate` срабатывает самым первым среди классических lifecycle hooks Options API.

```javascript
export default {
  beforeCreate() {
    console.log("Компонент еще не инициализирован полностью");
  },
};
```

На этом этапе компонент уже создается, но реактивное состояние и методы еще не готовы для обычного использования.

## Что недоступно

```javascript
export default {
  data() {
    return { count: 0 };
  },
  beforeCreate() {
    // this.count еще не готов как обычное reactive-свойство
  },
};
```

Поэтому в `beforeCreate` редко пишут бизнес-логику.

## Vue 3 и Composition API

В Composition API отдельного `onBeforeCreate` нет. Код, который должен выполняться очень рано, обычно пишут прямо в `setup` или `<script setup>`.

```vue
<script setup>
console.log("Выполняется во время setup");
</script>
```

## Когда может встретиться

`beforeCreate` полезно знать для чтения старых Vue 2 проектов, плагинов и legacy-кода. В новом Vue 3 коде почти всегда выбирают `setup`.

## Мини-шпаргалка

- `beforeCreate` - ранний Options API hook.
- Вызывается до инициализации `data` и `methods`.
- В Vue 3 Composition API обычно заменяется `setup`.
- Для DOM он не подходит: DOM еще не смонтирован.
