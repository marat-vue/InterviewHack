# Что такое Pinia Persisted State?

> [!NOTE]
> Pinia Persisted State - это подход и популярный plugin для сохранения выбранного Pinia state между перезагрузками страницы. Обычно state сохраняют в `localStorage`, `sessionStorage` или cookies.

## Какую проблему решает persistence?

Pinia хранит state в памяти JavaScript-приложения. Если пользователь обновит страницу, память приложения очистится.

```txt
Pinia state -> reload page -> initial state
```

Persisted state сохраняет данные во внешнее browser storage:

```txt
Pinia state -> localStorage/sessionStorage/cookie -> reload -> hydrate store
```

## Что можно сохранять?

Хорошие кандидаты:

- theme;
- language;
- collapsed sidebar;
- cart draft;
- onboarding state;
- user preferences;
- selected organization id.

## Что нельзя сохранять бездумно?

Опасные кандидаты:

- access token;
- refresh token;
- password;
- персональные данные;
- права, которым backend потом слепо доверяет;
- большие списки данных;
- временные loading/error states.

Persisted state - это удобство UX, а не secure storage.

## Где находится plugin?

Чаще всего используют пакет:

```bash
npm install pinia-plugin-persistedstate
```

Он добавляет опцию `persist` в Pinia stores.

## Мини-шпаргалка

- Pinia state пропадает при reload.
- Persisted state сохраняет выбранные данные в storage.
- Обычно используют `pinia-plugin-persistedstate`.
- Сохранять нужно только безопасные и полезные поля.
- Tokens и секреты нельзя класть в browser storage без threat model.
