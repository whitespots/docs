# Host network driver

### Introduction

`host`: For standalone containers, remove network isolation between the container and the Docker host, and use the host’s networking directly. See [use the host network](https://docs.docker.com/network/host/).

{% hint style="info" %}
**Host networks** are best when the network stack should not be isolated from the Docker host, but you want other aspects of the container to be isolated.
{% endhint %}

{% hint style="warning" %}
**Use the host network only when it is clearly necessary. All network ports of the application will be available at the host level, which is a threat.**
{% endhint %}

The goal of this tutorial is to start a `nginx` container which binds directly to port 80 on the Docker host. From a networking point of view, this is the same level of isolation as if the `nginx` process were running directly on the Docker host and not in a container. However, in all other ways, such as storage, process namespace, and user namespace, the `nginx` process is isolated from the host.

### Prerequisites <a id="prerequisites"></a>

* This procedure requires port 80 to be available on the Docker host. To make Nginx listen on a different port, see the [documentation for the `nginx` image](https://hub.docker.com/_/nginx/)
* The `host` networking driver only works on Linux hosts, and is not supported on Docker Desktop for Mac, Docker Desktop for Windows, or Docker EE for Windows Server.

### Creating a container 

Create a `docker-compose.yml` file and inside it paste the following:

```text
version: "3.3"

services:
  nginx:
    image: nginx
    network_mode: "host"
```

Save it and then run `docker-compose up -d`

From there you can verify that the container is running by browsing to [http://localhost:80/.](http://localhost:80/.)

**Verify which process is bound to port 80**, using the `netstat` command. You need to use `sudo` because the process is owned by the Docker daemon user and you otherwise won’t be able to see its name or PID.

```text
sudo netstat -tulpn | grep :80
```

Result is not surprising: 

```text
root@ubuntu1-VirtualBox:~# sudo netstat -tulpn | grep :80
tcp   0    0 0.0.0.0:80      0.0.0.0:*   LISTEN      4027/nginx: master  
tcp6  0    0 :::80           :::*        LISTEN      4027/nginx: master  
tcp6  0    0 :::8001         :::*        LISTEN      1110/docker-proxy 
```

