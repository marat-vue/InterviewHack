# Какие ошибки бывают при работе с motion-v?

> [!NOTE]
> Частые ошибки Motion for Vue связаны с чрезмерными анимациями, отсутствием `key` в `AnimatePresence`, анимацией дорогих CSS-свойств, игнорированием reduced motion, созданием motion components внутри render и смешиванием CSS/Vue/Motion без ясной ответственности.

## Ошибка 1. Анимировать все подряд

Плохо:

```vue
<motion.div :whileHover="{ scale: 1.2, rotate: 20, y: -20 }" />
```

Если каждый элемент страницы двигается, интерфейс утомляет. Анимация должна объяснять состояние, направление, причинно-следственную связь или интерактивность.

## Ошибка 2. Забыть key в AnimatePresence

```vue
<AnimatePresence>
  <motion.div v-if="isOpen" :exit="{ opacity: 0 }" />
</AnimatePresence>
```

Лучше:

```vue
<AnimatePresence>
  <motion.div v-if="isOpen" key="modal" :exit="{ opacity: 0 }" />
</AnimatePresence>
```

`key` помогает Motion отслеживать, какой direct child входит или выходит.

## Ошибка 3. Анимировать дорогие свойства

Осторожно с:

- `width`;
- `height`;
- `top`;
- `left`;
- тяжелыми shadows;
- blur/filter на больших областях.

Чаще безопаснее:

- `opacity`;
- `x`;
- `y`;
- `scale`;
- `rotate`.

## Ошибка 4. Игнорировать reduced motion

Пользователь может включить reduced motion на уровне системы. Для parallax, больших перемещений и autoplay-анимаций нужно предусматривать более спокойную версию.

```typescript
const shouldReduceMotion = useReducedMotion();
```

## Ошибка 5. Создавать motion.create внутри template/render

Плохо:

```typescript
const MotionCard = motion.create(Card);
```

если это выполняется заново на каждый render.

Компонент нужно создавать на module/setup уровне, а не внутри шаблонной логики.

## Ошибка 6. Конфликтовать с CSS transition

Если Tailwind/CSS задает:

```html
class="transition-all duration-300"
```

и Motion одновременно анимирует те же свойства, движение может стать непредсказуемым. Разделяй ответственность: одно свойство - один animation owner.

## Ошибка 7. Использовать Motion вместо Vue state logic

Motion отвечает за визуальное движение, но не должен скрывать состояние приложения.

Плохо:

```txt
если элемент визуально улетел, значит он удален
```

Лучше:

```txt
Vue state решает, есть ли элемент
Motion решает, как он появляется/исчезает
```

## Мини-шпаргалка

- Анимация должна помогать UX.
- Для `AnimatePresence` нужны стабильные `key`.
- Предпочитай `opacity` и transforms.
- Уважай `prefers-reduced-motion`.
- Не создавай motion components на каждый render.
- Не анимируй одно и то же свойство одновременно CSS и Motion.
- State принадлежит Vue, движение принадлежит Motion.
