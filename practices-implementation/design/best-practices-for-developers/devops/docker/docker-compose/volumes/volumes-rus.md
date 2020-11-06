# Volumes \(rus\)

### Создание и управление volume'ами <a id="create-and-manage-volumes"></a>

В отличии от bind mount, volume можно создать за пределами контейнера.

**Создать volume**:

```bash
$ docker volume create my-vol
```

**Показать все volumes**:

```bash
$ docker volume ls

local               my-vol
```

### Запустить контейнер с volume <a id="start-a-container-with-a-volume"></a>

Если запустить контейнер с volume, который не существует, Docker создаст его. Следующий пример демонстрирует монтирование volume `myvol2` в директорию `/app/` контейнера.

```bash
$ docker run -d \
  --name devtest \
  --mount source=myvol2,target=/app \
  nginx:latest
```

Выполните `docker inspect devtest` чтобы удостовериться, что volume был создан и монтирован в контейнер корректно. Смотрите секцию `Mounts` :

```bash
"Mounts": [
    {
        "Type": "volume",
        "Name": "myvol2",
        "Source": "/var/lib/docker/volumes/myvol2/_data",
        "Destination": "/app",
        "Driver": "local",
        "Mode": "",
        "RW": true,
        "Propagation": ""
    }
],
```

Остановите контейнер и удалите volume. Обратите внимание, что удаление volume'a является отдельным шагом:

```bash
$ docker container stop devtest

$ docker container rm devtest

$ docker volume rm myvol2
```

### Используйте volume с docker-compose <a id="use-a-volume-with-docker-compose"></a>

Docker compose сервис с volume выглядит так:

```bash
version: "3.8"
services:
  frontend:
    image: node:lts
    volumes:
      - myapp:/home/node/app
volumes:
  myapp:
```

При первом запуске`docker-compose up` ,  будет создан volume. Этот же volume будет использован при следующих запусках.

### Резервное копирование и восстановление

Volumes удобны при резервном копировании, восстановлении и миграциях. Используйте флаг `--volumes-from` для создания нового контейнера, который использует volume.

#### Резервное копирование  <a id="backup-a-container"></a>

Например, создайте новый контейнер `dbstore`:

```bash
$ docker run -v /dbdata --name dbstore ubuntu /bin/bash
```

Следующей командой мы:

* Запустим контейнер и монтируем в него volume из контейнера `dbstore` 
* Монтируем директорию локальной машины - `/backup`
* Передадим команду, которая архивирует содержимое volume'а `dbdata`  в файл `backup.tar`в директории `/backup` .

```bash
$ docker run --rm --volumes-from dbstore -v $(pwd):/backup ubuntu tar cvf /backup/backup.tar /dbdata
```

Когда команда выполнится, контейнер остановится и мы получим резевную копию volume'a  `dbdata` .

#### Восстановление из резервной копии <a id="restore-container-from-backup"></a>

Можно восстановить контейнер и его volume из созданной резервной копии используя этот же контейнер или любой другой

Например, создадим контейнер `dbstore2`:

```bash
$ docker run -v /dbdata --name dbstore2 ubuntu /bin/bash
```

И распакуем содержимое `backup.tar`в volume нового контейнера:

```bash
$ docker run --rm --volumes-from dbstore2 -v $(pwd):/backup ubuntu bash -c "cd /dbdata && tar xvf /backup/backup.tar --strip 1"
```



