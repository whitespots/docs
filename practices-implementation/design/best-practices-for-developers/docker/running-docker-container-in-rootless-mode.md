---
description: >-
  Rootless mode allows running the Docker containers as a non-root user to
  mitigate potential vulnerabilities.
---

# Running Docker container in rootless mode

## How it works

To run docker container as non-root user, you need to specify a user:group inside Dockerfile:

```text
RUN addgroup -S testgroup && adduser -S -G testuser testgroup
```

Specify your user:

```text
USER testuser
```

Example Dockerfile:

```text
FROM ruby:2.4-alpine
ARG VER=4.10.0
RUN addgroup -S testgroup && adduser -S -G testuser testgroup

RUN gem install brakeman -v $VER

USER testuser
```

{% hint style="info" %}
If you need to run Docker itself in rootless mode, check our guide [Running docker in rootless mode in ubuntu](running-docker-in-rootless-mode-in-ubuntu/)
{% endhint %}



