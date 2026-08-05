# Какие ошибки бывают при persisted state?

> [!NOTE]
> Persisted state часто ломает приложение не технически, а архитектурно: сохраняют лишнее, хранят секреты, получают устаревшие данные, конфликтуют с backend truth или забывают про SSR.

## Ошибка 1. Сохранять весь auth store

```typescript
persist: true
```

для auth store может сохранить:

- access token;
- user profile;
- permissions;
- loading flags;
- error messages.

Это почти всегда плохая идея. Auth должен проектироваться отдельно: session cookie, refresh flow, token rotation, backend validation.

## Ошибка 2. Доверять persisted permissions

Если в storage лежит:

```json
{
  "role": "admin"
}
```

это не значит, что пользователь admin. Browser storage контролируется пользователем. Backend обязан проверять права сам.

## Ошибка 3. Сохранять большие списки

```typescript
products: Product[]
```

Большие массивы в `localStorage`:

- замедляют старт;
- могут устареть;
- имеют ограничение по размеру;
- усложняют invalidation.

Для server data часто лучше использовать query cache или повторный API-запрос.

## Ошибка 4. Не думать про logout

При logout нужно очищать persisted state:

```typescript
settingsStore.$reset();
localStorage.removeItem("auth");
```

Иначе следующий пользователь на этом же устройстве может увидеть старые настройки или данные.

## Ошибка 5. Не учитывать private mode и quota

Storage может быть недоступен или переполнен. Критичная логика приложения не должна полностью зависеть от успешной записи в `localStorage`.

## Мини-шпаргалка

- Не сохраняй весь store автоматически.
- Не храни секреты в browser storage без threat model.
- Не доверяй roles/permissions из persisted state.
- Большие server datasets лучше не класть в `localStorage`.
- При logout очищай persisted данные.
- SSR и private mode требуют осторожности.
