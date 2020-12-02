# Bridge network driver

`bridge`: The default network driver. If you don’t specify a driver, this is the type of network you are creating. **Bridge networks are usually used when your applications run in standalone containers that need to communicate.** See [bridge networks](https://docs.docker.com/network/bridge/) docker docs page.

{% hint style="info" %}
**User-defined bridge networks** are best when you need multiple containers to communicate on the same Docker host.
{% endhint %}

{% hint style="warning" %}
There is also an option to use default `bridge` network, which is considered a legacy detail of Docker and is not recommended for production use. 
{% endhint %}

**User-defined bridges provide better isolation**.

All containers without a `network` specified, are attached to the default bridge network. This can be a risk, as unrelated stacks/services/containers are then able to communicate.

Using a user-defined network provides a scoped network in which only containers attached to that network are able to communicate.

**User-defined bridges provide automatic DNS resolution between containers**.

Containers on the default bridge network can only access each other by IP addresses, unless you use the [`--link` option](https://docs.docker.com/network/links/), which is considered legacy. On a user-defined bridge network, containers can resolve each other by name or alias.

**Containers can be attached and detached from user-defined networks on the fly**.

During a container’s lifetime, you can connect or disconnect it from user-defined networks on the fly. To remove a container from the default bridge network, you need to stop the container and recreate it with different network options.

**Each user-defined network creates a configurable bridge**.

If your containers use the default bridge network, you can configure it, but all the containers use the same settings, such as MTU and `iptables` rules. In addition, configuring the default bridge network happens outside of Docker itself, and requires a restart of Docker.

User-defined bridge networks are created and configured using `docker network create`. If different groups of applications have different network requirements, you can configure each user-defined bridge separately, as you create it.

**All ports are available on the same user-defined network**

Containers connected to the same user-defined bridge network effectively expose all ports to each other. For a port to be accessible to containers or non-Docker hosts on different networks, that port must be _published_ using the `-ports:` under `services:` section, for example:

```text
 webserver:
     image: nginx:1.15.12-alpine
     ports:
       - "8000:80"
       - "443:443"
```

**Linked containers on the default bridge network share environment variables**.

Originally, the only way to share environment variables between two containers was to link them using the [`--link` flag](https://docs.docker.com/network/links/). This type of variable sharing is not possible with user-defined networks. However, there are superior ways to share environment variables. A few ideas:

* Multiple containers can mount a file or directory containing the shared information, using a Docker volume.
* Multiple containers can be started together using `docker-compose` and the compose file can define the shared variables.
* You can use swarm services instead of standalone containers, and take advantage of shared [secrets](https://docs.docker.com/engine/swarm/secrets/) and [configs](https://docs.docker.com/engine/swarm/configs/).

### Manage a user-defined bridge <a id="manage-a-user-defined-bridge"></a>

Use the `docker network create` command to create a user-defined bridge network.

```text
$ docker network create my-net
```

You can specify the subnet, the IP address range, the gateway, and other options. Use the output of `docker network create --help` for details.

### Connect a container to a user-defined bridge <a id="connect-a-container-to-a-user-defined-bridge"></a>

This example connects a sample `wordpress`container to the `my-net` network.  Any other container connected to the `my-net` network has access to all ports on the `wordpress` container, and vice versa.                                                                                                                                                                                                                           

```text
version: '3.3'

services:
   db:
     image: mysql:5.7
     container_name: db       
     volumes:
       - db_data:/var/lib/mysql
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: somewordpress
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD: wordpress

   wordpress:
     depends_on:
       - db
     image: wordpress:latest
     container_name: wordpress
     networks:
       - default
     restart: always
     environment:
       WORDPRESS_DB_HOST: db:3306
       WORDPRESS_DB_USER: wordpress
       WORDPRESS_DB_PASSWORD: wordpress
       WORDPRESS_DB_NAME: wordpress
volumes:
    db_data:
networks:
  default:
    external:
      name: my-net
```

 Now we'll create another container on this network to make sure these ports are available by calling `container_name` using `nc` and `wget` commands:

```text
version: '3.3'

services:
   ubuntu:
     image: ubuntu:latest
     networks:
       - default
     volumes:
       - type: volume
         source: ubuntu
         target: /data
     command: bash -c "
       apt-get update &&
       apt-get install -y netcat &&
       apt-get install -y wget &&
       nc -zv wordpress 80 &&
       wget wordpress"
networks:
   default:
     external:
       name: my-net  
volumes:
   ubuntu:
```

Result should be like this:

```text
ubuntu_1  | Connection to wordpress 80 port [tcp/*] succeeded!
ubuntu_1  | --2020-12-02 12:08:28--  http://wordpress/
ubuntu_1  | Resolving wordpress (wordpress)... 172.20.0.3
ubuntu_1  | Connecting to wordpress (wordpress)|172.20.0.3|:80... connected.
ubuntu_1  | HTTP request sent, awaiting response... 302 Found
ubuntu_1  | Location: http://wordpress/wp-admin/install.php [following]
ubuntu_1  | --2020-12-02 12:08:28--  http://wordpress/wp-admin/install.php
ubuntu_1  | Reusing existing connection to wordpress:80.
ubuntu_1  | HTTP request sent, awaiting response... 200 OK
```

But we won't be able to connect using another network. Let's create a network  `my-net_2` , use it in the previous section with `nc` and `wget` commands and recheck: 

```text
...
       apt-get install -y netcat &&
       apt-get install -y wget &&
       nc -zv wordpress 80 &&
       wget wordpress"
networks:
   default:
     external:
       name: my-net_2
```

Result is not surprising 

```text
ubuntu_1  | nc: getaddrinfo for host "wordpress" port 80: Name or service not known
wordpress_2_ubuntu_1 exited with code 1
```

