# Android checks

## What to check while development

* Execution of Javascript in WebView is disabled
* There is no way to send any object to WebView
* ContentProvider's without signatures are not used
* There are no custom permissions without signatures
* OAuth scope **mobile:all** is not used
* OAuth tokens are sending only in request headers
* Domain without cookies is used for API backend
* OAuth token scopes are checking on backend
* Manifest attribute, which denies sending data in plain text is set \(**android:usesCleartextTraffic=”false”**\)
* There are no self-written TrustManagers
* There are no custom settings in certificate domain checking \(example: **ALLOW\_ALL\_HOSTNAME\_VERIFIER**\) or self-written HostnameVerifier's
* Class **SSLSocket** is not used for working with TLS
* There is an attribute in manifest, which allows to install the app only in internal storage \(**android:installLocation="internalOnly"**\)
* AccountManager is updated
* WebView does not exist
* App does not send PendingIntent's to another apps or services
* There is no way to send files/mails/etc, which links are sent from a user/intent
* The app is not storing any data on SD-Card
* The app is using code obfuscation with ProGuard, DexProtector and same solutions
* The custom keyboard is not used on critical inputs \(password/card number..\)

### Android applications security assessment

* Best practices for Android [http://developer.android.com/training/best-security.html](http://developer.android.com/training/best-security.html).
* Security features overview [http://source.android.com/tech/security/index.html](http://source.android.com/tech/security/index.html).
* Basic security assessment guides [http://www.mcafee.com/us/resources/white-papers/foundstone/wp-pen-testing-android-apps.pdf](http://www.mcafee.com/us/resources/white-papers/foundstone/wp-pen-testing-android-apps.pdf).

### Insecure Data Storage

* What information is stored in public databases?
* What information is stored on the SD-Card?
* Does the application verify that it was transferred to the SD card?

External storage is used by all applications that have requested access to it. Moreover, such resolution is completely ordinary and one of the most common. Therefore, if our application stores critical information on the SD card without encryption, this is a serious vulnerability.

* From snapshots of the virtual machine, we determine which publicly accessible files \(with reading rights for all\) the application created and what is in these files. If the data is critical, then they need to be encrypted or transferred to the built-in storage of the phone.
* Checking content providers \(see the code injection block\)
* It is also necessary to pay attention to what data remains in the application when the user logs out. If the user is logged out, there should be no critical user data in the application.

### Server-side assessment

* If the application was developed as stand-alone, this type of threat is absent for it.

Most applications use the webhooks of large services, but there are other interaction protocols \(XMPP, WebDAV, etc.\)

* If you use methods using the HTTP / HTTPS protocols, then we use our standard assessment methods for web services.
* Try to change the data that is stored on the backend.
* Use Burp suite and Python
* App can send **OAuth tokens** only in request headers
* For API backend use domain without any cookies

### Network dump analysis

* What information does the application transmit?
* You need to understand if encryption is required and in what cases.
* And also, does the application correctly handle invalid certificates when establishing an SSL connection?
* For **SSLFactory** need to use **STRICT\_HOSTNAME\_VERIFIER** mode for strict certificates checking.
* Verify that the exchange of login / password pairs for the OAuth token occurs via HTTPS.
* To intercept traffic, the most convenient way is to use an emulator with the following launch options:

```text
emulator -tcpdump traffic.cap -avd myvm
```

* After that, we look for phone identifiers, OAuth tokens, user personal data transmitted in clear form in traffic. Besides translating all network connectivity to HTTPS
* Also, starting with version 23, the android attribute has appeared in Android manifests **android:usesCleartextTraffic=”false”** which can be added to the **application** element. [https://security.googleblog.com/2016/04/protecting-against-unintentional.html](https://security.googleblog.com/2016/04/protecting-against-unintentional.html) He will tell Android that it is necessary to block data transfer in the clear \(only if the Android HTTP stack is used\).
* While developing or testing the application, you can use [https://developer.android.com/intl/ru/reference/android/os/StrictMode.html](https://developer.android.com/intl/ru/reference/android/os/StrictMode.html) StrictMode API for detecting traffic transmitted in a clear text.

### Client code injection

* If the application tries to display or play some local or backend files on the phone, you need to make sure that code cannot be injected through such user files.

The main danger arises when we try to display data using the device’s web browser. Here we can use a traditional XSS. If HTML / JS is opened from the built-in SD card and phone memory - it is possible to read local files.

* For Android, we need to pay special attention to content providers and see if they are not closed with privileges. Need to have a look at:

```text
**<provider 
android:enabled=["true" | "false"]
android:exported=["true" | "false"]
android:grantUriPermissions=["true" | "false"]
android:name="string"
android:permission="string"
android:readPermission="string"android:writePermission="string" >
. . .
</provider>**
```

If open, then check for SQL injection in them and critical data reading.

### Auth assessment

[https://habr.com/post/423753/](https://habr.com/post/423753/)

### User input

* It is important to understand what kind of intents the application has, and where the launch starts.
* What events \(intent's\) does the application process \(use intent sniffer\)?

1. Is the access restricted to your events using permissions?.
2. Check that broadcast system events are handled safely.
3. Check that broadcast system events contain no critical data

* What privilege levels are requested [https://developer.android.com/reference/android/Manifest.permission.html](https://developer.android.com/reference/android/Manifest.permission.html), Are they really required? Check manifest for it:

```text
<uses-permission android:name="android.permission.*" />
```

* Check for MODE\_WORLD\_READABLE or MODE\_WORLD\_WRITEABLE for sensitive files and DB.

### Data leakages

* How does logging work

A known and difficult error in the Android privilege system is the ability to access read system log files with a single privilege. At the same time, in various application builds there is a problem with excessive logging of debugging information in the production environment.

* Therefore, you need to make sure that logs do not contain:

1. Phone ID's
2. Logins/Passwords/Tokens.
3. PII \(client coordinates, contacts, SMS etc\).
4. Excessive details about the functioning of the application, some names of functions and methods, class names, etc

* Need to install the app in emulator and to work with it \(with logs saving\) After that just to grep some OAuth tokens, IMEI etc. We can also check it in code: Find **android.util.Log** and check **Log.i\(\), Log.d\(\), Log.w\(\), Log.e\(\), Log.wtf\(\)** usage

### Information exposure

* Check your code and .apk files.

Look for sensitive info in Strings resources

### Automate your checks

{% page-ref page="useful-tools/services/mobsf.md" %}

### Tools

* Mercury \([http://labs.mwrinfosecurity.com/tools/2012/03/16/mercury/](http://labs.mwrinfosecurity.com/tools/2012/03/16/mercury/)\) For DB and intents
* Intent fuzzer \([http://www.isecpartners.com/mobile-security-tools/intent-fuzzer.html](http://www.isecpartners.com/mobile-security-tools/intent-fuzzer.html)\) Fuzzer for intents. Good toolkit is placed here [http://www.isecpartners.com/mobile-security-tools/](http://www.isecpartners.com/mobile-security-tools/)
* Drozer \([https://labs.mwrinfosecurity.com/tools/drozer/](https://labs.mwrinfosecurity.com/tools/drozer/)\) Dynamic analysis
* MobSF \([https://github.com/MobSF/Mobile-Security-Framework-MobSF](https://github.com/MobSF/Mobile-Security-Framework-MobSF)\) Static + dynamic analysis

