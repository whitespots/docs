# Запуск Docker контейнера без root-прав

## Как это работает

Чтобы запустить докер контейнер от лица пользователя без root-привилегий, необходимо создать пользователя и группу используя Dockerfile:

```text
RUN addgroup -S testgroup && adduser -S -G testuser testgroup
```

Укажите пользователя:

```text
USER testuser
```

Пример файла Dockerfile:

```text
FROM ruby:2.4-alpine
ARG VER=4.10.0
RUN addgroup -S testgroup && adduser -S -G testuser testgroup

RUN gem install brakeman -v $VER

USER testuser
```

{% hint style="info" %}
Если необходимо запустить непосредственно докер от пользователя без root-привилегий, смотрите нашу инструкцию [Запуск docker в режиме rootless на ubuntu](../running-docker-in-rootless-mode-in-ubuntu/zapusk-docker-v-rezhime-rootless-na-ubuntu.md) 
{% endhint %}

