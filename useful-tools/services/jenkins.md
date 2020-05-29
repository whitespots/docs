---
description: Manage your scripts in CI/CD
---

# Jenkins

## Mac OS

```text
brew install jenkins
brew services (re)start jenkins
brew upgrade jenkins
```

## Docker

```text
sudo -i
    
apt install apt-transport-https ca-certificates curl gnupg-agent software-properties-common -y
    
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

add-apt-repository \
"deb [arch=amd64] https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) \
stable"

apt-get update

apt-get install docker-ce docker-ce-cli containerd.io -y

curl -L https://github.com/docker/compose/releases/download/1.23.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose

wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
apt update
apt install openjdk-11-jdk jenkins -y
systemctl start jenkins
sudo usermod -aG docker jenkins

cat /var/lib/jenkins/secrets/initialAdminPassword
```

Then use the password from stdout on your [http://ip:8080/](http://ip:8080/) page

**Pipeline example**

```text
node {
   stage('Secrets hunting') { 
     sh '/usr/local/bin/trufflehog --json --regex --max_depth=20 --entropy=False $github_repo > secrets.json'
   }
   stage('Results') {
      archiveArtifacts 'secrets.json'
   }
}
```

## Have questions?

Write to us and get a **free** consultation.

**Website**: [whitespots.io](https://whitespots.io/?utm=appsecwiki)   
**Email**: [sales@whitespots.io](mailto:sales@whitespots.io)

