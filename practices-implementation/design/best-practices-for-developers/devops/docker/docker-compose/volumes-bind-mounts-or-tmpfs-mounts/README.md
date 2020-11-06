# Volumes, bind mounts or tmpfs mounts

### Problem with managing data in Docker 

By default all files created inside a container are stored on a writable container layer. This means that:

* The data doesn’t persist when that container no longer exists.
* A container’s writable layer is tightly coupled to the host machine where the container is running. You can’t easily move the data somewhere else.
* Writing into a container’s writable layer requires a [storage driver](https://docs.docker.com/storage/storagedriver/) to manage the filesystem. The storage driver provides a union filesystem, using the Linux kernel. This extra abstraction reduces performance as compared to using _data volumes_, which write directly to the host filesystem.

Docker has two options for containers to store files in the host machine, so that the files are persisted even after the container stops: _volumes_, and _bind mounts_. If you’re running Docker on Linux you can also use a _tmpfs mount_.

### Choose the right type of mount

Depends on what you need, you can choose between 3 ways of storing your data:

![](../../../../../../../.gitbook/assets/image%20%284%29.png)

* **Volumes** are stored in a part of the host filesystem which is _managed by Docker_ \(`/var/lib/docker/volumes/` on Linux\). Non-Docker processes should not modify this part of the filesystem. Volumes are the best way to persist data in Docker.
* **Bind mounts** may be stored _anywhere_ on the host system. They may even be important system files or directories. Non-Docker processes on the Docker host or a Docker container can modify them at any time.
* **`tmpfs` mounts** are stored in the host system’s memory only, and are never written to the host system’s filesystem.

{% hint style="info" %}
Detailed information about mount types can be found on [docker docs page](https://docs.docker.com/storage/#more-details-about-mount-types).
{% endhint %}

### Good use cases:

#### Volumes

Volumes are the preferred way to persist data in Docker containers and services. Some use cases for volumes include:

* Sharing data among multiple running containers. If you don’t explicitly create it, a volume is created the first time it is mounted into a container. When that container stops or is removed, the volume still exists. Multiple containers can mount the same volume simultaneously, either read-write or read-only. Volumes are only removed when you explicitly remove them.
* When the Docker host is not guaranteed to have a given directory or file structure. Volumes help you decouple the configuration of the Docker host from the container runtime.
* When you want to store your container’s data on a remote host or a cloud provider, rather than locally.
* When you need to back up, restore, or migrate data from one Docker host to another, volumes are a better choice. You can stop containers using the volume, then back up the volume’s directory \(such as `/var/lib/docker/volumes/<volume-name>`\).
* When your application requires high-performance I/O on Docker Desktop. Volumes are stored in the Linux VM rather than the host, which means that the reads and writes have much lower latency and higher throughput.
* When your application requires fully native file system behavior on Docker Desktop. For example, a database engine requires precise control over disk flushing to guarantee transaction durability. Volumes are stored in the Linux VM and can make these guarantees, whereas bind mounts are remoted to macOS or Windows, where the file systems behave slightly differently.

#### Bind mounts

In general, you should use volumes where possible. Bind mounts are appropriate for the following types of use case:

* Sharing configuration files from the host machine to containers. This is how Docker provides DNS resolution to containers by default, by mounting `/etc/resolv.conf` from the host machine into each container.
* Sharing source code or build artifacts between a development environment on the Docker host and a container. For instance, you may mount a Maven `target/` directory into a container, and each time you build the Maven project on the Docker host, the container gets access to the rebuilt artifacts.

  If you use Docker for development this way, your production Dockerfile would copy the production-ready artifacts directly into the image, rather than relying on a bind mount.

* When the file or directory structure of the Docker host is guaranteed to be consistent with the bind mounts the containers require.

#### Tmpfs mounts

`tmpfs` mounts are best used for cases when you do not want the data to persist either on the host machine or within the container. This may be for security reasons or to protect the performance of the container when your application needs to write a large volume of non-persistent state data.

