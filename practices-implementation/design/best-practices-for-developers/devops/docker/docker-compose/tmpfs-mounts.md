# tmpfs mounts

If you’re running Docker on Linux, you have a third option: `tmpfs` mounts. When you create a container with a `tmpfs` mount, the container can create files outside the container’s writable layer.

As opposed to volumes and bind mounts, a `tmpfs` mount is temporary, and only persisted in the host memory. When the container stops, the `tmpfs` mount is removed, and files written there won’t be persisted.

This is useful to temporarily store sensitive files that you don’t want to persist in either the host or the container writable layer.

### Limitations of tmpfs mounts <a id="limitations-of-tmpfs-mounts"></a>

* Unlike volumes and bind mounts, you can’t share `tmpfs` mounts between containers.
* This functionality is only available if you’re running Docker on Linux.

### Use a tmpfs mount in a container <a id="use-a-tmpfs-mount-in-a-container"></a>

```text
$ docker run -d \
  -it \
  --name tmptest \
  --mount type=tmpfs,destination=/app \
  nginx:latest
```

Verify that the mount is a `tmpfs` mount by running `docker container inspect tmptest` and looking for the `Mounts` section:

```text
"Tmpfs": {
    "/app": ""
},
```

Remove the container:

```text
$ docker container stop tmptest

$ docker container rm tmptest
```

#### Specify tmpfs options <a id="specify-tmpfs-options"></a>

`tmpfs` mounts allow for two configuration options, neither of which is required.

| Option | Description |
| :--- | :--- |
| `tmpfs-size` | Size of the tmpfs mount in bytes. Unlimited by default. |
| `tmpfs-mode` | File mode of the tmpfs in octal. For instance, `700` or `0770`. Defaults to `1777` or world-writable. |

The following example sets the `tmpfs-mode` to `1770`, so that it is not world-readable within the container.

```text
docker run -d \
  -it \
  --name tmptest \
  --mount type=tmpfs,destination=/app,tmpfs-mode=1770 \
  nginx:latest
```

### Use a bind mount with docker-compose

Mount a temporary file system inside the container. Size parameter specifies the size of the tmpfs mount in bytes. Unlimited by default.

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
For more information on tmpfs mounts visit Docker Docs [page](https://docs.docker.com/storage/tmpfs/).
{% endhint %}

