# Ключевое слово `continue`

> [!NOTE] Коротко
> `continue` пропускает оставшуюся часть текущей итерации цикла и сразу переходит к следующей.

## Вопрос

Что делает ключевое слово `continue`?

## Пример

```javascript
for (let i = 1; i <= 5; i++) {
  if (i === 3) continue;

  console.log(i);
}
```

Результат:

```text
1
2
4
5
```

Когда `i === 3`, строка `console.log(i)` пропускается.

## Где можно использовать

`continue` работает только в циклах:

```javascript
for (...) {}
while (...) {}
do (...) while (...);
```

В `switch` использовать `continue` нельзя, если `switch` не находится внутри цикла.

## Практический пример

```javascript
const users = [
  { name: "Anna", active: true },
  { name: "Max", active: false },
  { name: "Kate", active: true },
];

for (const user of users) {
  if (!user.active) continue;

  console.log(user.name);
}
```

Так можно пропускать неподходящие элементы.

## `continue` vs `break`

```javascript
for (let i = 1; i <= 5; i++) {
  if (i === 3) continue; // пропустить 3
}
```

```javascript
for (let i = 1; i <= 5; i++) {
  if (i === 3) break; // остановить цикл на 3
}
```

## Мини-шпаргалка

| Ключевое слово | Что делает |
| --- | --- |
| `continue` | перейти к следующей итерации |
| `break` | выйти из цикла |
| `return` | выйти из функции |
