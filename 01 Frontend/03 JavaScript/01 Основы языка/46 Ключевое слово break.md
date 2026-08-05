# Ключевое слово `break`

> [!NOTE]
> `break` досрочно завершает цикл или `switch` и передает управление на код после этой конструкции.

## Вопрос

Что делает ключевое слово `break`?

## В цикле

```javascript
for (let i = 1; i <= 5; i++) {
  if (i === 3) break;

  console.log(i);
}
```

Результат:

```text
1
2
```

Когда `i === 3`, цикл завершается полностью.

## В `while`

```javascript
let attempts = 0;

while (true) {
  attempts++;

  if (attempts === 3) {
    break;
  }
}
```

`break` часто используют, чтобы выйти из потенциально бесконечного цикла.

## В `switch`

```javascript
switch (role) {
  case "admin":
    console.log("Полный доступ");
    break;
  case "user":
    console.log("Обычный доступ");
    break;
}
```

Без `break` выполнение провалится в следующие `case`.

## `break` vs `continue`

`break` завершает весь цикл.

```javascript
if (value === null) break;
```

`continue` завершает только текущую итерацию.

```javascript
if (value === null) continue;
```

## С метками

`break` может выходить из внешнего цикла через label.

```javascript
outer: for (const row of matrix) {
  for (const cell of row) {
    if (cell === target) {
      break outer;
    }
  }
}
```

Используется редко, но иногда полезно для вложенных циклов.

## Мини-шпаргалка

| Где | Что делает |
| --- | --- |
| `for` | завершает цикл |
| `while` | завершает цикл |
| `do...while` | завершает цикл |
| `switch` | выходит из `switch` |
| `label` | может выйти из отмеченного блока/цикла |
