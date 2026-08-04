# Как работать с images pull build tag push?

> [!NOTE]
> Основной цикл работы с images: скачать через `docker pull`, собрать через `docker build`, присвоить имя и tag через `docker tag`, отправить в registry через `docker push`.

## Скачать image

```bash
docker pull node:22-alpine
docker pull postgres:18
docker pull nginx:alpine
```

Формат:

```text
repository:tag
```

Если tag не указан, Docker часто использует `latest`, но в production лучше фиксировать конкретную версию.

## Собрать image

```bash
docker build -t my-api:1.0.0 .
```

Здесь:

- `-t` - имя и tag image;
- `.` - build context;
- Docker ищет `Dockerfile` в context.

## Указать Dockerfile явно

```bash
docker build -f docker/Dockerfile -t my-api .
```

Полезно, если Dockerfile лежит не в корне проекта.

## Посмотреть images

```bash
docker image ls
```

История слоев:

```bash
docker image history my-api:1.0.0
```

## Tag image

```bash
docker tag my-api:1.0.0 registry.example.com/team/my-api:1.0.0
```

Tag не копирует image. Он добавляет еще одно имя к тому же image ID.

## Push image

```bash
docker push registry.example.com/team/my-api:1.0.0
```

Перед этим обычно нужен login:

```bash
docker login registry.example.com
```

## Почему latest опасен?

`latest` - это просто tag, а не гарантия самой новой или стабильной версии.

Плохо:

```yaml
image: my-api:latest
```

Лучше:

```yaml
image: my-api:1.14.3
```

В production еще лучше использовать digest:

```text
my-api@sha256:...
```

## Что отвечать на собеседовании?

Images скачивают через `docker pull`, собирают через `docker build`, помечают через `docker tag` и публикуют через `docker push`. Image имеет repository и tag. `latest` - это обычный tag, поэтому для production лучше использовать конкретные версии или digest.

## Частые ошибки

- Считать `latest` надежной версией.
- Пушить image без правильного registry prefix.
- Не понимать, что tag не пересобирает image.
- Собирать image из слишком большого build context.
- Не проверять, какие layers попали в image.

## Мини-шпаргалка

- `docker pull image:tag` - скачать.
- `docker build -t name:tag .` - собрать.
- `docker tag old new` - дать новое имя.
- `docker push name:tag` - отправить в registry.
- `docker image ls` - список images.
- `latest` не означает безопасность.
