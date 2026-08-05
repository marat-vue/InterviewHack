# Что такое $router.push?

> [!NOTE]
> `$router.push` или `router.push` программно переводит пользователя на другой маршрут и добавляет новую запись в историю браузера.

## Вопрос

Что такое `$router.push`?

## Options API

```javascript
export default {
  methods: {
    goToProfile() {
      this.$router.push("/profile");
    },
  },
};
```

`this.$router` доступен, если приложение подключило Vue Router.

## Composition API

```typescript
import { useRouter } from "vue-router";

const router = useRouter();

function goToProfile() {
  router.push("/profile");
}
```

## Навигация по имени маршрута

```typescript
router.push({
  name: "user",
  params: { id: "42" },
  query: { tab: "settings" },
});
```

Именованные маршруты удобнее, если path может поменяться.

## push против replace

`push` добавляет запись в историю, а `replace` заменяет текущую.

```typescript
router.replace("/login");
```

После `replace` кнопка Back не вернет на замененный маршрут.

## Мини-шпаргалка

- `router.push()` делает программный переход.
- В Options API: `this.$router.push`.
- В Composition API: `useRouter().push`.
- Для замены текущей записи есть `router.replace`.
