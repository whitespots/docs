# tmpfs mounts \(rus\)

Если Docker запущен на Linux, то открывается возможность использовать  `tmpfs` mount. При создании контейнера с  `tmpfs` mount, контейнер может создавать файлы вне контейнера.

В отличии от  volumes и bind mounts,  `tmpfs` mount является временным хранилищем и хранится только в оперативной памяти хост-машины. Когда контейнер останавливается, `tmpfs` mount удаляется и все файлы удаляются вместе с ним. 

Это удобно для хранения секретов, которые нежелательно хранить на хост-машине или в памяти контейнера. 

### Ограничения tmpfs mount <a id="limitations-of-tmpfs-mounts"></a>

* В отличии от volume и bind mount, `tmpfs` mount нельзя использовать в ряде контейнеров.
* Этот функционал доступен только на Linux.

### Использование tmpfs mount в контейнере <a id="use-a-tmpfs-mount-in-a-container"></a>

```text
$ docker run -d \
  -it \
  --name tmptest \
  --mount type=tmpfs,destination=/app \
  nginx:latest
```

Проверьте, работает ли  `tmpfs` mount запустив команду `docker container inspect tmptest` Смотрите секцию `Mounts` :

```text
"Tmpfs": {
    "/app": ""
},
```

Удалить контейнер:

```text
$ docker container stop tmptest

$ docker container rm tmptest
```

#### Укажите опции tmpfs mount <a id="specify-tmpfs-options"></a>

`tmpfs` mount принимает два параметра, ни один из них не является необходимым.

| Параметр   | Описание |
| :--- | :--- |
| `tmpfs-size` | Размер tmpfs mount в байтах. Не ограничен по умолчанию. |
| `tmpfs-mode` | File mode для tmpfs mount в восьмиричной системе. Можно использовать, `700` или `0770`. По умолчанию установлено `1777` , доступно для записи всем. |

Следующий пример устанавливает значение `1770` для параметра `tmpfs-mode` ограничивая чтение bind mount для всех, кроме контейнера. 

```text
docker run -d \
  -it \
  --name tmptest \
  --mount type=tmpfs,destination=/app,tmpfs-mode=1770 \
  nginx:latest
```

### Использование bind mount с docker-compose

Пример ниже монтирует временную файловую систему внутри контейнера. Параметр size устанавливает размер контейнера в байтах. Mode ограничивает чтение файловой системы для всех, кроме контейнера.

```text
version: "3.8"
services:
  web:
    image: nginx:alpine
    volumes:
      - type: tmpfs
        target: /app
        tmpfs:
          size: 1000
          mode: 1770
```

{% hint style="info" %}
Для получения подробной информации о  tmpfs mount, смотрите [страницу](https://docs.docker.com/storage/tmpfs/) документации Docker.
{% endhint %}

