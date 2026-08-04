# `break` в `switch`

> [!NOTE] Коротко
> `break` останавливает выполнение `switch` после нужного `case`. Если его не поставить, произойдет fall-through: JavaScript продолжит выполнять следующие `case`.

## Вопрос

Что делает `break` в `switch`? Что произойдет, если не использовать `break` внутри `switch`?

## Как работает `switch`

```javascript
switch (status) {
  case "loading":
    console.log("Загрузка");
    break;
  case "success":
    console.log("Готово");
    break;
  default:
    console.log("Неизвестный статус");
}
```

Когда найден подходящий `case`, выполняется его код. `break` выводит выполнение за пределы `switch`.

## Что будет без `break`

```javascript
const day = "mon";

switch (day) {
  case "mon":
    console.log("Понедельник");
  case "tue":
    console.log("Вторник");
  default:
    console.log("Другой день");
}
```

Результат:

```text
Понедельник
Вторник
Другой день
```

Это называется fall-through.

## Когда fall-through используют осознанно

Иногда несколько `case` должны делать одно и то же.

```javascript
switch (day) {
  case "sat":
  case "sun":
    console.log("Выходной");
    break;
  default:
    console.log("Рабочий день");
}
```

Здесь отсутствие `break` между `sat` и `sun` намеренное.

## `default`

`default` срабатывает, если не найден ни один `case`.

```javascript
switch (role) {
  case "admin":
    access = "full";
    break;
  default:
    access = "none";
}
```

После `default` тоже можно поставить `break`, особенно если ниже есть другие `case`.

## Мини-шпаргалка

```javascript
case "value":
  doSomething();
  break; // выйти из switch
```

| Ситуация | Поведение |
| --- | --- |
| `break` есть | выполнение `switch` завершается |
| `break` нет | выполнение идет в следующий `case` |
| несколько пустых `case` подряд | общий обработчик |
| `default` | ветка по умолчанию |
