# Что такое "состояния" в CSS-анимациях?

> [!NOTE]
> **Состояния** в CSS - это разные визуальные варианты элемента: обычный, hover, focus, active, disabled, open, error, loading. Анимации и переходы помогают плавно менять элемент между этими состояниями.

## Главное

CSS часто описывает не только базовый вид, но и состояние.

```css
.button {
  background: #2563eb;
  transform: translateY(0);
  transition: transform 150ms ease, background 150ms ease;
}

.button:hover {
  background: #1d4ed8;
  transform: translateY(-2px);
}
```

Здесь есть базовое состояние и состояние `:hover`.

## Частые состояния

| Состояние | Пример |
| --- | --- |
| Наведение | `:hover` |
| Фокус | `:focus-visible` |
| Нажатие | `:active` |
| Отключение | `:disabled` |
| Отмечено | `:checked` |
| Ошибка | `.is-error` |
| Загрузка | `.is-loading` |

## Состояния через классы

```css
.accordion__panel {
  max-height: 0;
  overflow: hidden;
  transition: max-height 200ms ease;
}

.accordion.is-open .accordion__panel {
  max-height: 320px;
}
```

JavaScript может добавлять класс `.is-open`, а CSS плавно меняет состояние.

## Состояния и доступность

Нельзя полагаться только на hover. Пользователь клавиатуры должен видеть focus-состояние.

```css
.button:focus-visible {
  outline: 3px solid #2563eb;
  outline-offset: 2px;
}
```

## Мини-шпаргалка

- Состояние - визуальный вариант элемента.
- Псевдоклассы описывают нативные состояния.
- Классы вроде `.is-open` описывают состояние компонента.
- Transition плавно меняет состояние.
- Hover не заменяет focus.
