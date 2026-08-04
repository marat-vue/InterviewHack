# Что такое media query. Для чего они используются?

> [!NOTE]
> **Media query** - это CSS-условие, которое применяет стили только при определенных характеристиках устройства или среды: ширине viewport, типе устройства, ориентации, hover-возможностях и пользовательских настройках.

## Главное

```css
@media (max-width: 768px) {
  .layout {
    grid-template-columns: 1fr;
  }
}
```

Это правило сработает, если viewport не шире `768px`.

## Mobile-first пример

```css
.layout {
  display: grid;
  gap: 16px;
}

@media (min-width: 768px) {
  .layout {
    grid-template-columns: 240px 1fr;
  }
}
```

База для мобильных, расширение для больших экранов.

## Что можно проверять

```css
@media (orientation: landscape) {
  .hero {
    min-height: 80vh;
  }
}

@media (hover: hover) {
  .card:hover {
    transform: translateY(-2px);
  }
}

@media (prefers-reduced-motion: reduce) {
  * {
    animation-duration: 0.01ms;
  }
}
```

Media queries полезны не только для ширины.

## Комбинации условий

```css
@media (min-width: 768px) and (max-width: 1199px) {
  .sidebar {
    display: none;
  }
}
```

Можно комбинировать несколько условий через `and`.

## Мини-шпаргалка

- Media query применяет CSS по условию.
- Частые условия: `min-width`, `max-width`.
- Mobile-first обычно использует `min-width`.
- Можно проверять ориентацию, hover, motion preferences.
- Media queries нужны для крупных изменений layout.
- Fluid-подход может уменьшить количество breakpoints.
