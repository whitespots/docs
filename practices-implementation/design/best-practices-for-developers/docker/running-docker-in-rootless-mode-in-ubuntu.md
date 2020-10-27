---
description: >-
  Rootless mode allows running the Docker daemon and containers as a non-root
  user to mitigate potential vulnerabilities in the daemon and the container
  runtime.
---

# Running docker in rootless mode in ubuntu

## How it works

Rootless mode executes the Docker daemon and containers inside a user namespace. This is very similar to [`userns-remap` mode](https://docs.docker.com/engine/security/userns-remap/), except that with `userns-remap` mode, the daemon itself is running with root privileges, whereas in rootless mode, both the daemon and the container are running without root privileges.

Rootless mode does not use binaries with `SETUID` bits or file capabilities, except `newuidmap` and `newgidmap`, which are needed to allow multiple UIDs/GIDs to be used in the user namespace.

## Prerequisites

* You must install `newuidmap` and `newgidmap` on the host. These commands are provided by the `uidmap` package on most distros.
* `/etc/subuid` and `/etc/subgid` should contain at least 65,536 subordinate UIDs/GIDs for the user. In the following example, the user `testuser` has 65,536 subordinate UIDs/GIDs \(231072-296607\).

```text
$ id -u
1001
$ whoami
testuser
$ grep ^$(whoami): /etc/subuid
testuser:231072:65536
$ grep ^$(whoami): /etc/subgid
testuser:231072:65536
```

## Install

```text
$ curl -fsSL https://get.docker.com/rootless | sh
```

Make sure to run the script as a non-root user. To install Rootless Docker as the root user, see the [Manual installation](https://docs.docker.com/engine/security/rootless/#manual-installation) steps.

The script shows environment variables that are required:

```text
$ curl -fsSL https://get.docker.com/rootless | sh
...
# Docker binaries are installed in /home/testuser/bin
# WARN: dockerd is not in your current PATH or pointing to /home/testuser/bin/dockerd
# Make sure the following environment variables are set (or add them to ~/.bashrc):

export PATH=/home/testuser/bin:$PATH
export PATH=$PATH:/sbin
export DOCKER_HOST=unix:///run/user/1001/docker.sock

#
# To control docker service run:
# systemctl --user (start|stop|restart) docker
#
```

## Usage

### Daemon

Use `systemctl --user` to manage the lifecycle of the daemon:

```text
$ systemctl --user start docker
```

To launch the daemon on system startup, enable the systemd service and lingering:

```text
$ systemctl --user enable docker
$ sudo loginctl enable-linger $(whoami)
```

### Client

You need to specify the socket path explicitly.

To specify the socket path using `$DOCKER_HOST`:

```text
$ echo "export DOCKER_HOST=unix://$XDG_RUNTIME_DIR/docker.sock" >> ~/.profile
```

{% hint style="warning" %}
After this step you must logout and login again
{% endhint %}

And finally, run nginx container:

```text
$ docker run -d -p 8080:80 nginx
```

Check your user with `ps auxf`:

![](../../../../.gitbook/assets/docker-rootless.png)

{% hint style="info" %}
Full guide with distributive specific hints can be found on Docker Docs page \([Run the Docker daemon as a non-root user](https://docs.docker.com/engine/security/rootless/)\)
{% endhint %}

