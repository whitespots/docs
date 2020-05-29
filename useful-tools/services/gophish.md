---
description: Phishing automation for free
---

# GoPhish

## Docker install

```text
sudo -i

apt install apt-transport-https ca-certificates curl gnupg-agent software-properties-common -y

curl -fsSL <https://download.docker.com/linux/ubuntu/gpg> | sudo apt-key add -

add-apt-repository \\
   "deb [arch=amd64] <https://download.docker.com/linux/ubuntu> \\
   $(lsb_release -cs) \\
   stable"

apt-get update

apt-get install docker-ce docker-ce-cli containerd.io docker-compose -y
```

## Gophish

```text
docker run -d --name gophish -p 3333:3333 -p 80:80 matteoggl/gophish
```



