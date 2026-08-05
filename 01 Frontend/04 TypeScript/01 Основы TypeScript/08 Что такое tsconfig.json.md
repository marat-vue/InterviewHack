# Что такое tsconfig.json?

> [!NOTE]
> `tsconfig.json` - файл настроек TypeScript-проекта: какие файлы проверять и как компилировать код.

## Вопрос

Для чего нужен `tsconfig.json`?

## Определение

`tsconfig.json` сообщает TypeScript-компилятору, где находится проект и какие правила проверки использовать. В нем задают `compilerOptions`, список файлов, исключения и особенности сборки.

Если в папке есть `tsconfig.json`, TypeScript воспринимает ее как корень проекта.

## Пример

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "ESNext",
    "strict": true,
    "noEmit": true
  },
  "include": ["src"]
}
```

## Частые поля

| Поле | Что делает |
| --- | --- |
| `target` | версия JavaScript на выходе |
| `module` | формат модулей |
| `strict` | включает строгие проверки |
| `noEmit` | проверять типы без генерации JS |
| `include` | какие файлы включить |
| `exclude` | какие файлы исключить |

## strict

```json
{
  "compilerOptions": {
    "strict": true
  }
}
```

Для обучения и серьезных проектов лучше привыкать к `strict: true`.

## Мини-шпаргалка

```json
{
  "compilerOptions": {
    "strict": true
  },
  "include": ["src"]
}
```
