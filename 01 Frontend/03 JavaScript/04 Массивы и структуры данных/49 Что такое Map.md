# Что такое Map?

> [!NOTE] Коротко
> `Map` - коллекция пар "ключ-значение", где ключом может быть значение любого типа, включая объект.

## Вопрос

Когда использовать `Map` вместо обычного объекта?

## Определение

`Map` хранит данные как пары `key -> value`. В отличие от объекта, ключами могут быть не только строки и `Symbol`, но и числа, объекты, функции, `NaN` и другие значения.

`Map` также сохраняет порядок добавления элементов и имеет удобное свойство `size`.

## Базовый пример

```javascript
const userRoles = new Map();

const user = { id: 1 };

userRoles.set(user, 'admin');
userRoles.set('guest', 'reader');

console.log(userRoles.get(user)); // 'admin'
console.log(userRoles.has(user)); // true
console.log(userRoles.size);      // 2
```

## Основные методы

```javascript
map.set(key, value); // добавить или обновить
map.get(key);        // получить значение
map.has(key);        // проверить наличие ключа
map.delete(key);     // удалить пару
map.clear();         // очистить все
```

## Перебор Map

```javascript
const prices = new Map([
  ['apple', 100],
  ['banana', 80],
]);

for (const [product, price] of prices) {
  console.log(product, price);
}
```

## Map vs Object

| Критерий | Object | Map |
| --- | --- | --- |
| Типы ключей | строки и `Symbol` | любые значения |
| Размер | `Object.keys(obj).length` | `map.size` |
| Порядок | есть правила порядка ключей | порядок вставки |
| Частые добавления/удаления | не всегда удобно | удобно |

## Мини-шпаргалка

```javascript
const map = new Map();

map.set('name', 'Ann');
map.get('name'); // 'Ann'
map.has('name'); // true
map.size;        // 1
```
