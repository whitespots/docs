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

## Mailserver install

```text
docker pull tvial/docker-mailserver:latest
mkdir mailserver
cd mailserver
curl -o setup.sh <https://raw.githubusercontent.com/tomav/docker-mailserver/master/setup.sh;> chmod a+x ./setup.sh
curl -o docker-compose.yml <https://raw.githubusercontent.com/tomav/docker-mailserver/master/docker-compose.yml.dist>
curl -o .env <https://raw.githubusercontent.com/tomav/docker-mailserver/master/.env.dist>
curl -o env-mailserver <https://raw.githubusercontent.com/tomav/docker-mailserver/master/env-mailserver.dist>

docker-compose up -d mail

# create user login
./setup.sh email add <user@domain> [<password>]

# configure dkim
./setup.sh config dkim
public is here -> config/opendkim/keys/domain.tld/mail.txt
cat config/opendkim/keys/domain.tld/mail.txt
```

## Gophish

```text
docker run -d --name gophish -p 3333:3333 -p 80:80 matteoggl/gophish
```

## Have questions?

Write to us and get a **free** consultation.

**Website**: [whitespots.io](https://whitespots.io/?utm=appsecwiki)   
**Email**: [sales@whitespots.io](mailto:sales@whitespots.io)

