# Bypasses

## Auth

### **JWT**

Symmetric algorithms are vulnerable to the local bruteforce attack.

* HS256
* HS512
* HS...

You can try to brute such algorithms to issue a new JWT.

### **Password reset links**

They can be:

* Predictable You need to know the generation algorithm to generate your own link
* Reusable Try to look for leaked tokens
* Leaked 90% you can see them in some marketing systems

### **Custom logic**

* Reinvented session algorithms All sessions must be at least:

  * Not predictable
  * Unique
  * Revocable
  * Time limited

  Are you sure, that you did not forget about all such properties in your custom algorithm?

* Custom cryptography, based on obscurity Try to get the app source code and all such security will fall

## Rate limits

```text
X-Originating-IP: 127.0.0.1
X-Forwarded-For: 127.0.0.1
X-Forwarded-Host: 127.0.0.1
X-Remote-IP: 127.0.0.1
X-Remote-Addr: 127.0.0.1

#or use double X-Forwared-For header
X-Forwarded-For:
X-Forwarded-For: 127.0.0.1

Forwarded: for=127.0.0.1; host=127.0.0.1
```

## Filters

### **Dot & digits**

[http://⑯⑨](http://xn--wrhn)。②⑤④。⑯⑨｡②⑤④/

[http://⓪ⓧⓐ⑨](http://xn--wrhznmcl)｡⓪ⓧⓕⓔ｡⓪ⓧⓐ⑨｡⓪ⓧⓕⓔ:80/

[http://⓪ⓧⓐ⑨ⓕⓔⓐ⑨ⓕⓔ:80/](http://xn--wrha42abtcdd9m3a:80/)

[http://②⑧⑤②⓪③⑨①⑥⑥:80/](http://xn--orhbaeijakm21k:80/)

[http://④②⑤](http://xn--prhde)｡⑤①⓪｡④②⑤｡⑤①⓪:80/

[http://⓪②⑤①](http://xn--orhbj84c)。⓪③⑦⑥。⓪②⑤①。⓪③⑦⑥

![](../../.gitbook/assets/image%20%281%29.png)

### **Quote**

* DB
  * $$
  * CHR\(39\)
* %27 / %22

## Special characters

### Dot

```text
evil.com = evil。com = evil%25E3%2580%2582com
```

### Slashes

```text
Python example (2 slashes in advance are for this language escaping)
/ = \\\\\\\\x2f
\\ = \\\\\\\\x5c
```

### Spaces

```text
SQL:
' ' = + = /**/
```

### Quotes

```text
SQL:
' = $$
JS:
' = `
```

### Other

![](../../.gitbook/assets/image%20%282%29.png)

```text
< ~ %e2%89%ae
< ~ %ef%b9%a4
< ~ %ef%bc%9c
> ~ %u226e
> ~ %e2%89%af
> ~ %ef%b9%a5
> ~ %ef%bc%9e
```

\([https://appcheck-ng.com/unicode-normalization-vulnerabilities-the-special-k-polyglot/\#](https://appcheck-ng.com/unicode-normalization-vulnerabilities-the-special-k-polyglot/#)\)

