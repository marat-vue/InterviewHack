# Как типизировать Pinia store?

> [!NOTE]
> Pinia хорошо выводит типы автоматически, но для пустых массивов, nullable data и сложных объектов лучше явно помогать TypeScript через interfaces, type aliases и начальные значения.

## Типизация state

```typescript
interface User {
  id: number;
  email: string;
  role: "user" | "admin";
}

interface AuthState {
  user: User | null;
  isLoading: boolean;
}

export const useAuthStore = defineStore("auth", {
  state: (): AuthState => ({
    user: null,
    isLoading: false,
  }),
});
```

Так TypeScript понимает, что `user` может быть `null`.

## Пустые массивы

```typescript
state: () => ({
  users: [] as User[],
});
```

Без подсказки TypeScript может вывести слишком узкий тип для пустого массива.

## Типизация actions

```typescript
actions: {
  async login(payload: LoginPayload): Promise<void> {
    const user = await authApi.login(payload);
    this.user = user;
  },
}
```

Payload лучше описывать отдельно:

```typescript
interface LoginPayload {
  email: string;
  password: string;
}
```

## Getters и this

Если getter использует `this`, иногда нужно явно указать return type:

```typescript
getters: {
  isAdmin(): boolean {
    return this.user?.role === "admin";
  },
}
```

## Store type в composables

Обычно не нужно вручную писать тип store. Используй результат функции:

```typescript
const authStore = useAuthStore();
```

Если нужен тип:

```typescript
type AuthStore = ReturnType<typeof useAuthStore>;
```

## Мини-шпаргалка

- Pinia хорошо infer-ит типы.
- Для `null` и пустых массивов помогай TypeScript явно.
- Actions типизируй через payload interfaces.
- Getters с `this` иногда требуют return type.
- Тип store можно получить через `ReturnType<typeof useStore>`.
