# Что такое слот в Vue?

> [!NOTE]
> Слот - это место внутри дочернего компонента, куда родитель передает свой шаблон. Слоты делают компоненты гибкими и переиспользуемыми.

## Вопрос

Что такое слот в Vue?

## Базовый пример

```vue
<!-- BaseCard.vue -->
<template>
  <article class="card">
    <slot />
  </article>
</template>
```

```vue
<!-- Parent.vue -->
<template>
  <BaseCard>
    <h2>Профиль</h2>
    <p>Основная информация</p>
  </BaseCard>
</template>
```

Контент внутри `<BaseCard>` попадает на место `<slot />`.

## Контент по умолчанию

```vue
<template>
  <button>
    <slot>Отправить</slot>
  </button>
</template>
```

Если родитель ничего не передал, будет показано `Отправить`.

## Именованные слоты

```vue
<template>
  <header><slot name="header" /></header>
  <main><slot /></main>
  <footer><slot name="footer" /></footer>
</template>
```

```vue
<BaseLayout>
  <template #header>Заголовок</template>
  Контент страницы
  <template #footer>Подвал</template>
</BaseLayout>
```

## Когда использовать

Слоты подходят для карточек, модалок, layout-компонентов, таблиц и wrapper-компонентов, где структура общая, а содержимое разное.

## Мини-шпаргалка

- `<slot />` - точка вставки родительского шаблона.
- Можно задать fallback-контент.
- `#name` - короткая запись для именованного слота.
- Slots передают разметку, props передают данные.
