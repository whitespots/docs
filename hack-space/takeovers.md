# Takeovers

## Domain

### NS

* dig NS **@8.8.8.8** [yoursite.com](http://yoursite.com)
* dig NS **@ns-1307.awsdns-60.org** [yoursite.com](http://yoursite.com)

If you have the **NXDOMAIN** status, but root dns does not know about it and has some NS servers where you should look for your record - congrats, you have a domain takeover

### CNAME

* dig CNAME **@8.8.8.8** [yoursite.com](http://yoursite.com)
* dig [anyother.com](http://anyother.com)

If you have the **NXDOMAIN** status in the target CNAME domain - it's also a domain takeover.

More details about takeovers you can read here [https://www.hackerone.com/blog/Guide-Subdomain-Takeovers](https://www.hackerone.com/blog/Guide-Subdomain-Takeovers)

## Account

### Social networks linking

* Site with a personal area
* Connect facebook feature

Just try to link your attacker facebook account to the testing account, but do it carefully with the burp intercepter tab. Then copy your return-url and give it to your victim.

[Profit](http://wisdomfreak.com/2020/05/account-takeover-using-oauth-misconfiguration/)

