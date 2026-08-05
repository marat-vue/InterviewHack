# Безопасность и innerHTML

> [!NOTE]
> `innerHTML` опасен с пользовательскими данными, потому что строка интерпретируется как HTML и может привести к XSS.

## Вопрос

Почему нельзя бездумно вставлять пользовательский ввод через `innerHTML`?

## Определение

XSS, Cross-Site Scripting, - уязвимость, при которой злоумышленник внедряет вредоносный JavaScript в страницу. `innerHTML` может стать источником XSS, если вставлять в него непроверенную строку.

## Опасный пример

```javascript
const comment = document.querySelector('.comment');

comment.innerHTML = userInput;
```

Если `userInput` содержит HTML, браузер попытается его распарсить.

## Безопаснее для текста

```javascript
const comment = document.querySelector('.comment');

comment.textContent = userInput;
```

`textContent` вставляет строку как текст, а не как HTML-разметку.

## Безопасное создание DOM

```javascript
const link = document.createElement('a');

link.textContent = 'Profile';
link.href = '/profile';

container.append(link);
```

Создание элементов через DOM API часто безопаснее и точнее, чем сборка HTML-строки.

## Когда innerHTML допустим

- разметка полностью контролируется разработчиком;
- данные очищены надежным sanitizer-ом;
- нужно быстро заменить большой фрагмент известного HTML.

## Практическое правило

Если данные пришли от пользователя, сервера, URL или внешнего источника, не вставляй их в `innerHTML` без очистки.

## Мини-шпаргалка

```javascript
element.textContent = userText; // безопаснее
element.innerHTML = trustedHtml; // только доверенный HTML
```
