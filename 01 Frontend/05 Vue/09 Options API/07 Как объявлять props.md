# Как объявлять props?

> [!NOTE]
> В Options API props объявляют в опции `props`. Можно указать массив имен или объект с типами, обязательностью, default values и validator.

## Вопрос

Как объявлять props в Options API?

## Простая форма

```javascript
export default {
  props: ["title", "disabled"],
};
```

Такой вариант короткий, но почти ничего не документирует.

## Объектная форма

```javascript
export default {
  props: {
    title: {
      type: String,
      required: true,
    },
    size: {
      type: String,
      default: "md",
    },
  },
};
```

Эта запись понятнее: видно тип, обязательность и значение по умолчанию.

## Validator

```javascript
props: {
  variant: {
    type: String,
    default: "primary",
    validator(value) {
      return ["primary", "secondary"].includes(value);
    },
  },
}
```

Validator помогает ограничить допустимые значения на runtime.

## Использование

```vue
<template>
  <button :class="`button-${variant}`">
    {{ title }}
  </button>
</template>
```

Props доступны в шаблоне напрямую и через `this` в методах.

## Мини-шпаргалка

- `props: ["name"]` - короткая форма.
- Объектная форма лучше документирует контракт.
- `required`, `default`, `validator` уточняют prop.
- Props нельзя мутировать напрямую.
