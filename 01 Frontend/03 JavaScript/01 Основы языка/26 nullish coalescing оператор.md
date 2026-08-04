# Nullish coalescing operator `??`

> [!NOTE] Коротко
> `??` возвращает правое значение только тогда, когда левое равно `null` или `undefined`. В отличие от `||`, он не заменяет `0`, `false` и пустую строку.

## Вопрос

Что делает оператор `??` (nullish coalescing)?

## Синтаксис

```javascript
const result = value ?? fallback;
```

Если `value` не `null` и не `undefined`, вернется `value`. Иначе вернется `fallback`.

```javascript
null ?? "default";      // "default"
undefined ?? "default"; // "default"
0 ?? "default";         // 0
false ?? "default";     // false
"" ?? "default";        // ""
```

## Главное отличие от `||`

`||` смотрит на truthy/falsy.

```javascript
0 || 10;  // 10
"" || "Без имени"; // "Без имени"
false || true; // true
```

`??` смотрит только на `null` и `undefined`.

```javascript
0 ?? 10;  // 0
"" ?? "Без имени"; // ""
false ?? true; // false
```

## Когда использовать

`??` полезен, когда `0`, `false` или `""` являются нормальными значениями.

```javascript
function createPagination(page) {
  const currentPage = page ?? 1;

  return currentPage;
}

createPagination(0);         // 0
createPagination(undefined); // 1
```

## С optional chaining

`??` часто используют вместе с `?.`.

```javascript
const city = user?.address?.city ?? "Город не указан";
```

Если цепочка сломается и вернет `undefined`, сработает значение по умолчанию.

## Ограничение синтаксиса

`??` нельзя смешивать с `||` или `&&` без скобок.

```javascript
// SyntaxError
const value = a ?? b || c;
```

Правильно:

```javascript
const value = (a ?? b) || c;
```

## Мини-шпаргалка

| Выражение | Результат |
| --- | --- |
| `null ?? "x"` | `"x"` |
| `undefined ?? "x"` | `"x"` |
| `0 ?? "x"` | `0` |
| `"" ?? "x"` | `""` |
| `false ?? "x"` | `false` |
