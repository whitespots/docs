# Bind mounts

### Start a container with a bind mount <a id="start-a-container-with-a-bind-mount"></a>

```text
$ docker run -d \
  -it \
  --name devtest \
  -v "$(pwd)"/target:/app \
  nginx:latest
```

### Stop the container:

```text
$ docker container stop devtest

$ docker container rm devtest
```

### Mount into a non-empty directory on the container

{% hint style="warning" %}
If you bind-mount into a non-empty directory on the container, the directory’s existing contents are obscured by the bind mount. 
{% endhint %}

This can be beneficial, such as when you want to test a new version of your application without building a new image.

This example is contrived to be extreme, but replaces the contents of the container’s `/usr/` directory with the `/tmp/` directory on the host machine. In most cases, this would result in a non-functioning container.

```text
$ docker run -d \
  -it \
  --name broken-container \
  -v /tmp:/usr \
  nginx:latest

docker: Error response from daemon: oci runtime error: container_linux.go:262:
starting container process caused "exec: \"nginx\": executable file not found in $PATH".
```

### Use a read-only bind mount <a id="use-a-read-only-bind-mount"></a>

{% hint style="info" %}
For some development applications, the container needs to write into the bind mount, so changes are propagated back to the Docker host. At other times, the container only needs read access.
{% endhint %}

This example mounts the directory as a read-only bind mount, by adding `ro` to the \(empty by default\) list of options, after the mount point within the container. 

```text
$ docker run -d \
  -it \
  --name devtest \
  -v "$(pwd)"/target:/app:ro \
  nginx:latest
```

Use `docker inspect devtest` to verify that the bind mount was created correctly. Look for the `Mounts` section:

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

Stop the container:

```text
$ docker container stop devtest

$ docker container rm devtest
```

### Use a bind mount with docker-compose

A single docker compose service with a bind mount looks like this:

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
When creating bind mounts, using the long syntax requires the referenced folder to be created beforehand. For short syntax, if needed, search for "Short syntax" on [this](https://docs.docker.com/compose/compose-file/) Docker Docs page.
{% endhint %}

{% hint style="info" %}
For more information on bind mounts visit Docker Docs [page](https://docs.docker.com/storage/bind-mounts/).
{% endhint %}

