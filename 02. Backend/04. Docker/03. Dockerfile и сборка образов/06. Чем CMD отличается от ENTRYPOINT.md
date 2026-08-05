# Чем CMD отличается от ENTRYPOINT?

> [!NOTE]
> `CMD` задает команду по умолчанию для контейнера, а `ENTRYPOINT` задает основной executable. Часто `ENTRYPOINT` фиксирует программу, а `CMD` задает аргументы по умолчанию.

## CMD

```dockerfile
CMD ["node", "dist/main.js"]
```

`CMD` легко переопределяется:

```bash
docker run my-api node dist/worker.js
```

В этом случае вместо `node dist/main.js` выполнится новая команда.

## ENTRYPOINT

```dockerfile
ENTRYPOINT ["node"]
CMD ["dist/main.js"]
```

Теперь:

```bash
docker run my-api dist/worker.js
```

будет интерпретироваться как:

```bash
node dist/worker.js
```

## Exec form и shell form

Лучше использовать exec form:

```dockerfile
CMD ["node", "dist/main.js"]
```

Менее предпочтительно:

```dockerfile
CMD node dist/main.js
```

Exec form лучше работает с сигналами и не добавляет лишнюю shell-обертку.

## Когда использовать CMD?

Для обычных сервисов:

```dockerfile
CMD ["npm", "start"]
```

Например API, frontend server, worker.

## Когда использовать ENTRYPOINT?

Для CLI-tools:

```dockerfile
ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["postgres"]
```

Или:

```dockerfile
ENTRYPOINT ["node", "cli.js"]
```

Тогда container ведет себя как исполняемая команда.

## Что отвечать на собеседовании?

`CMD` задает default command или default arguments контейнера и легко переопределяется при `docker run`. `ENTRYPOINT` задает основной executable контейнера. Их можно комбинировать: `ENTRYPOINT` фиксирует программу, а `CMD` задает аргументы по умолчанию. Для большинства app containers достаточно `CMD`, для CLI-images часто используют `ENTRYPOINT`.

## Частые ошибки

- Путать build-time `RUN` и runtime `CMD`.
- Использовать shell form без причины.
- Делать сложный startup script вместо нормальной команды.
- Не понимать, почему аргументы `docker run image ...` заменили `CMD`.
- Использовать `ENTRYPOINT`, когда достаточно `CMD`.

## Мини-шпаргалка

- `RUN` - во время build.
- `CMD` - команда по умолчанию при run.
- `ENTRYPOINT` - основной executable.
- `CMD` можно заменить аргументами `docker run`.
- Exec form обычно лучше shell form.
- `ENTRYPOINT + CMD` удобно для CLI.
