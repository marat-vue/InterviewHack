# Как объявлять props в setup?

> [!NOTE]
> В `<script setup>` props объявляют через `defineProps`. В обычном `setup(props)` props приходят первым аргументом.

## Вопрос

Как объявлять props в `setup`?

## script setup с TypeScript

```vue
<script setup lang="ts">
type User = {
  id: number;
  name: string;
};

const props = defineProps<{
  user: User;
  isActive?: boolean;
}>();
</script>
```

Такой вариант дает хороший type checking и автодополнение.

## Значения по умолчанию

```vue
<script setup lang="ts">
const props = withDefaults(
  defineProps<{
    size?: "sm" | "md" | "lg";
  }>(),
  {
    size: "md",
  }
);
</script>
```

`withDefaults` задает default values для опциональных props.

## Runtime-объявление

```vue
<script setup>
const props = defineProps({
  title: {
    type: String,
    required: true,
  },
});
</script>
```

Такой вариант похож на Options API и полезен без TypeScript.

## Обычный setup

```javascript
export default {
  props: {
    title: String,
  },
  setup(props) {
    console.log(props.title);
  },
};
```

## Мини-шпаргалка

- В `<script setup>` используй `defineProps`.
- С TypeScript: `defineProps<{ ... }>()`.
- Defaults: `withDefaults`.
- Props readonly, не мутируй их напрямую.
