# Что такое two pointers?

> [!summary]
> Two pointers - паттерн, где два указателя движутся по массиву или строке, чтобы решить задачу за один проход или без вложенного цикла. Часто используется на отсортированных массивах, палиндромах и задачах с парами.

## Базовая идея

Вместо двух вложенных циклов:

```text
for i
  for j
```

двигаем два индекса:

```text
left ->          <- right
```

## Two sum на sorted array

```ts
function twoSumSorted(nums: number[], target: number): [number, number] | null {
  let left = 0
  let right = nums.length - 1

  while (left < right) {
    const sum = nums[left] + nums[right]

    if (sum === target) return [left, right]
    if (sum < target) left++
    else right--
  }

  return null
}
```

Time `O(n)`, space `O(1)`.

## Проверка палиндрома

```ts
function isPalindrome(s: string): boolean {
  let left = 0
  let right = s.length - 1

  while (left < right) {
    if (s[left] !== s[right]) return false
    left++
    right--
  }

  return true
}
```

## Когда узнавать паттерн?

- массив отсортирован;
- нужно найти пару;
- нужно сравнивать начало и конец;
- нужно удалить дубликаты in-place;
- нужно сжать строку/массив;
- brute force проверяет пары `O(n^2)`.

## Что отвечать на собеседовании?

Two pointers использует два индекса, которые двигаются по input. Он часто заменяет вложенный перебор пар на линейный проход, если есть порядок или понятное правило движения указателей. Например, в sorted two sum сумма меньше target - двигаем left, больше target - двигаем right.

## Частые ошибки

- Применять two pointers к неотсортированному массиву без основания.
- Не доказывать, почему можно двигать указатель.
- Ошибаться в условии `left < right`.
- Забывать edge cases пустой строки/массива.
- Двигать оба указателя сразу, когда нужно один.

## Мини-шпаргалка

- Два индекса.
- Часто `left/right`.
- Хорош для sorted arrays.
- Убирает `O(n^2)` pairs.
- Палиндромы - классика.
- Главное - правило движения.

## Связанные темы

- [[01 Что такое linear search и binary search]]
- [[02 Что такое sliding window]]
- [[3. Какие задачи нужно уметь решать]]
