# Network drivers

Docker’s networking subsystem is pluggable, using drivers. Several drivers exist by default, and provide core networking functionality. See docker networking overview on [Docker Docs page](https://docs.docker.com/network/). 

**Security summary** 

According to OWASP Security cheat sheet for Docker \([link to OWASP](https://cheatsheetseries.owasp.org/cheatsheets/Docker_Security_Cheat_Sheet.html)\), rule \#5 says "Disable inter-container communication \(--icc=false\)". 

{% hint style="danger" %}
**By default, containers are connected to default bridge network, therefore providing zero isolation between these containers, which can be a threat in the case of intrusion.** 
{% endhint %}

{% hint style="success" %}
Use user-defined bridge networks to provide isolation for your services. See our article on [bridge network driver](bridge-network-driver/) to check how it works. 
{% endhint %}

When using the host network driver, be sure to check which application ports are available and if they are configured securely. 

{% hint style="danger" %}
**Use the host network only when it is clearly necessary. All network ports of the application will be available at the host level, which can be a threat.**
{% endhint %}

{% hint style="success" %}
Host networks are best when the network stack should not be isolated from the Docker host, but you want other aspects of the container to be isolated. See our article on [host network driver](host-network-driver/) to check how it works. 
{% endhint %}

