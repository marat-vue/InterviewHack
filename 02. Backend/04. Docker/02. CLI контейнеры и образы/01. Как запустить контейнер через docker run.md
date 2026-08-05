# Как запустить контейнер через docker run?

> [!NOTE]
> `docker run` создает и запускает container из image. Через флаги можно задать имя, порт, переменные окружения, volume, сеть, режим detach и команду запуска.

## Минимальный запуск

```bash
docker run nginx:alpine
```

Docker:

1. ищет image локально;
2. если image нет, скачивает его из registry;
3. создает container;
4. запускает default command image.

## Запуск в фоне

```bash
docker run -d nginx:alpine
```

`-d` означает detached mode: контейнер работает в фоне, а terminal возвращает управление.

## Имя контейнера

```bash
docker run --name web nginx:alpine
```

Имя удобно использовать в командах:

```bash
docker logs web
docker stop web
docker rm web
```

## Проброс портов

```bash
docker run -d --name web -p 8080:80 nginx:alpine
```

Формат:

```text
host_port:container_port
```

Теперь можно открыть:

```text
http://localhost:8080
```

## Переменные окружения

```bash
docker run -e NODE_ENV=production -e PORT=3000 my-api
```

Для PostgreSQL:

```bash
docker run -d \
  --name db \
  -e POSTGRES_PASSWORD=secret \
  -p 5432:5432 \
  postgres:18
```

## Volume

```bash
docker run -d \
  --name db \
  -e POSTGRES_PASSWORD=secret \
  -v pgdata:/var/lib/postgresql/data \
  postgres:18
```

Так данные базы сохранятся после удаления container.

## Интерактивный режим

```bash
docker run -it ubuntu:24.04 bash
```

Флаги:

- `-i` - interactive;
- `-t` - pseudo-TTY.

## Удалить контейнер после остановки

```bash
docker run --rm node:22-alpine node -v
```

`--rm` полезен для одноразовых команд.

## Что отвечать на собеседовании?

`docker run` создает и запускает container из image. Самые важные флаги: `-d` для фонового режима, `--name` для имени, `-p` для проброса портов, `-e` для env, `-v` для volumes, `--rm` для одноразового контейнера и `-it` для интерактивной сессии.

## Частые ошибки

- Путать `8080:80` и `80:8080`.
- Забывать `-d` и думать, что контейнер завис.
- Не задавать volume для базы данных.
- Использовать `--rm` для контейнера, данные которого нужны.
- Ожидать, что `EXPOSE` сам опубликует порт на host.

## Мини-шпаргалка

- `docker run image` - создать и запустить.
- `-d` - background.
- `--name` - имя.
- `-p host:container` - порт.
- `-e KEY=value` - env.
- `-v volume:path` - storage.
- `--rm` - удалить после завершения.
