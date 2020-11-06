# Volumes

### Create and manage volumes <a id="create-and-manage-volumes"></a>

Unlike a bind mount, you can create and manage volumes outside the scope of any container.

**Create a volume**:

```bash
$ docker volume create my-vol
```

**List volumes**:

```bash
$ docker volume ls

local               my-vol
```

### Start a container with a volume <a id="start-a-container-with-a-volume"></a>

If you start a container with a volume that does not yet exist, Docker creates the volume for you. The following example mounts the volume `myvol2` into `/app/` in the container.

```bash
$ docker run -d \
  --name devtest \
  --mount source=myvol2,target=/app \
  nginx:latest
```

Use `docker inspect devtest` to verify that the volume was created and mounted correctly. Look for the `Mounts` section:

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

Stop the container and remove the volume. Note volume removal is a separate step.

```bash
$ docker container stop devtest

$ docker container rm devtest

$ docker volume rm myvol2
```

### Use a volume with docker-compose <a id="use-a-volume-with-docker-compose"></a>

A single docker compose service with a volume looks like this:

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

On the first invocation of `docker-compose up` the volume will be created. The same volume will be reused on following invocations.

### Backup and restore volumes

Volumes are useful for backups, restores, and migrations. Use the `--volumes-from` flag to create a new container that mounts that volume.

#### Backup a container <a id="backup-a-container"></a>

For example, create a new container named `dbstore`:

```bash
$ docker run -v /dbdata --name dbstore ubuntu /bin/bash
```

Then in the next command, we:

* Launch a new container and mount the volume from the `dbstore` container
* Mount a local host directory as `/backup`
* Pass a command that tars the contents of the `dbdata` volume to a `backup.tar` file inside our `/backup` directory.

```bash
$ docker run --rm --volumes-from dbstore -v $(pwd):/backup ubuntu tar cvf /backup/backup.tar /dbdata
```

When the command completes and the container stops, we are left with a backup of our `dbdata` volume.

#### Restore container from backup <a id="restore-container-from-backup"></a>

With the backup just created, you can restore it to the same container, or another that you made elsewhere.

For example, create a new container named `dbstore2`:

```bash
$ docker run -v /dbdata --name dbstore2 ubuntu /bin/bash
```

Then un-tar the backup file in the new container\`s data volume:

```bash
$ docker run --rm --volumes-from dbstore2 -v $(pwd):/backup ubuntu bash -c "cd /dbdata && tar xvf /backup/backup.tar --strip 1"
```



