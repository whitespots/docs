# Bind mounts \(rus\)

### Запуск контейнера с bind mount: <a id="start-a-container-with-a-bind-mount"></a>

```text
$ docker run -d \
  -it \
  --name devtest \
  -v "$(pwd)"/target:/app \
  nginx:latest
```

### Остановить контейнер:

```text
$ docker container stop devtest

$ docker container rm devtest
```

### Монтирование в директорию контейнера, не являющуюся пустой

{% hint style="warning" %}
Если монтировать bind-mount в директорию с файлами внутри контейнера, то содержимое директории будет недоступно внутри контейнера.
{% endhint %}

Это может быть удобно в случае, если необходимо проверить новую версию приложения без сборки нового контейнера.

Это утрированный пример, в нем содержимое директории контейнера `/usr/` перезаписывается директорией хост-машины `/tmp/` В большинстве случаев, такой шаг приведет к сломанному контейнеру. 

```text
$ docker run -d \
  -it \
  --name broken-container \
  -v /tmp:/usr \
  nginx:latest

docker: Error response from daemon: oci runtime error: container_linux.go:262:
starting container process caused "exec: \"nginx\": executable file not found in $PATH".
```

### Режим "только чтение" <a id="use-a-read-only-bind-mount"></a>

{% hint style="info" %}
Для некоторых приложений необходимо, чтобы контейнер писал в bind mount, чтобы изменения применялись на хост-машине, но бывает, что необходимо только чтение с хост-машины.
{% endhint %}

Этот пример монтирует директорию в режиме только для чтения через добавление `ro`  в список опций после директории для монтирования в контейнере.

```text
$ docker run -d \
  -it \
  --name devtest \
  -v "$(pwd)"/target:/app:ro \
  nginx:latest
```

Используйте `docker inspect devtest` чтобы удостовериться, что bind mount создан. Смотрите `Mounts` секцию:

```text
"Mounts": [
    {
        "Type": "bind",
        "Source": "/tmp/source/target",
        "Destination": "/app",
        "Mode": "ro",
        "RW": false,
        "Propagation": "rprivate"
    }
],
```

Остановить контейнер:

```text
$ docker container stop devtest

$ docker container rm devtest
```

### Использование bind mount с docker-compose

Простой docker сервис с bind mount выглядит так:

```text
version: "3.8"
services:
  web:
    image: nginx:alpine
    volumes:
      - type: bind
        source: ./static
        target: /opt/app/static
```

{% hint style="warning" %}
При использовании длинного синтаксиса bind mount директории не создаются автоматически, их необходимо создать до запуска контейнера, иначе контейнер не запустится. Для автоматического создания директорий необходимо использовать короткий синтаксис. Информацию о его использовании можно найти на [странице](https://docs.docker.com/compose/compose-file/) документации Docker. Ищите "short syntax" на странице. 
{% endhint %}

{% hint style="info" %}
Для получения подробной информации о  bind mount посетите [страницу](https://docs.docker.com/storage/bind-mounts/) документации Docker.
{% endhint %}

