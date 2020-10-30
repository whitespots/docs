# JWT Algorithms use cases

* **Integrity**: Nobody did change the data
* **Authenticity**: You can verify the origin of data
* **Non-repudiation \(from authority\)**: Not only you can verify the origin of data
* **Confidentiality**: Data is kept secret from unauthorised parties

### **Algorithm classes** 

| Name | Integrity | Confidentiality | Authenticity | Non-repudiation |
| :--- | :---: | :---: | :---: | :---: |
| HMAC | ✅ | 🚫 | ✅ | 🚫 |
| Authenticated encryption | ✅ | ✅ | ✅ | 🚫 |
| Digital signatures | ✅ | 🚫 | ✅ | ✅ |

### **Hash-based Message Authentication Code \(HMAC\)**

**Algorithms:**

* HS256
* HS384
* HS512

**Use cases:**

* Stateless sessions stored in browser cookies
* Email verification codes
* Session IDs with the ability to differentiate between expired and invalid IDs
* Tokens where issuer and ultimate consumer is the same party

Example JWT for a stateless session cookie:

```text
{
  "sub"      : "user-12345",
  "email"    : "alice@wonderland.net",
  "login_ip" : "172.16.254.1", 
  "exp"      : 1471102267
}
```

### Digital signatures

**Algorithms:**

[RSA signature with PKCS \#1 and SHA-2:](https://tools.ietf.org/html/rfc7518#section-3.3)

* RS256
* RS384
* RS512

[RSA PSS signature with SHA-2](https://tools.ietf.org/html/rfc7518#section-3.5):

* PS256
* PS384
* PS512

[EC DSA signature with SHA-2](https://tools.ietf.org/html/rfc7518#section-3.4):

* ES256
* ES384
* ES512

[Edwards-curve DSA signature with SHA-2](https://tools.ietf.org/html/rfc8037#section-3.1):

* Ed25519
* Ed448

**Use cases:**

* ID tokens \(OpenID Connect\)
* Self-contained access tokens \(OAuth 2.0\)
* Passing security assertions and tokens between domains
* Data which integrity and authenticity must be verifiable by others

### Authenticated encryption

**Algorithms:**

Public / private key encryption:

* RSA:
  * [RSA OAEP](https://tools.ietf.org/html/rfc7518#section-4.3):
    * RSA-OAEP
    * RSA-OAEP-256
  * [RSA PKCS \#1](https://tools.ietf.org/html/rfc7518#section-4.2):
    * RSA1\_5 \(deprecated due to [security vulnerability](https://en.wikipedia.org/wiki/Adaptive_chosen-ciphertext_attack)\)
* EC:
  * [ECDH-ES](https://tools.ietf.org/html/rfc7518#section-4.6) with EC or [OKP](https://tools.ietf.org/html/rfc8037#section-3.2) key:
    * ECDH-ES
    * ECDH-ES+A128KW
    * ECDH-ES+A192KW
    * ECDH-ES+A256KW

Secret \(shared\) key encryption:

* [Direct AES encryption](https://tools.ietf.org/html/rfc7518#section-4.5):
  * dir
* [AES key wrap](https://tools.ietf.org/html/rfc7518#section-4.4):
  * A128KW
  * A192KW
  * A256KW
* [AES GCM key encryption](https://tools.ietf.org/html/rfc7518#section-4.7):
  * A128GCMKW
  * A192GCMKW
  * A256GCMKW

Password based encryption:

* [PBES2](https://tools.ietf.org/html/rfc7518#section-4.8):
  * PBES2-HS256+A128KW
  * PBES2-HS384+A192KW
  * PBES2-HS512+A256KW

**Use cases:**

* Signed and encrypted ID tokens \(OpenID Connect\)
* Signed and encrypted self-contained access tokens \(OAuth 2.0\)
* Encrypted documents and data, with integrity and authenticity check

Example of JWE-header, payload will be encrypted with 128-bit AES in GCM, and AES CEK is encrypted with RSA \(RSA OAEP\):

```text
{
  "alg" : "RSA-OAEP",
  "enc" : "A128GCM"
}
```



