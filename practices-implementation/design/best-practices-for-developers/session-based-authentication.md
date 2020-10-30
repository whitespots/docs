# Session-based authentication

## Sessions must be

* Generated with crypto random and be unpredictable \([Exploit example](https://github.com/tna0y/Python-random-module-cracker)\)
* At least 128 bits \(16 bytes\) length according to [OWASP](https://owasp.org/www-community/vulnerabilities/Insufficient_Session-ID_Length)
* Stored in a cookie storage with all security flags \(secure, httponly, SameSite=Lax\)
* Sent via POST and **never** via GET method
* Generated on back-end and never be saved from a user input to prevent session fixation attacks
* Renewed with **any** privilege level change
* Invalidated with user logout
* Sent to clients with `cache-control: no-store` header
* Binded to user-agent

