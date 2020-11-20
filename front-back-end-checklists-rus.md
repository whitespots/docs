# ASVS V4: Чеклисты для управления, frontend и backend

## Управление 

### V1.1 Требования к процессу безопасной разработки \(SSDLC\)

**Средние и высокие требования:**

1. Принципы SSDLC используется на всех этапах разработки. 
2. Моделируются угрозы для каждого изменения в дизайне приложения или в спринтах планируется поиск угроз, планируются контрмеры и проводится тестирование на безопасность. 
3. Все пользовательские функции имеют ограничения безопасности, например "Я, как пользователь, могу просматривать и редактировать свой профиль. Я не должен видеть и редактировать чей-либо еще профиль"
4. Все точки доступа и доверия приложения, компонентов и значительных потоков данных документированы и их использование обосновано. 
5. Проведено определение и анализ высокоуровневой архитектуры приложения и всех подключенных удаленных сервисов. 
6. Внедрена централизованная, простая, проверенная, безопасная система контроля безопасности, чтобы избежать дублирования, отсутствия, неэффективного или небезопасного контроля. 
7. Всем разработчикам и тестировщикам доступны чек-листы, требования безопасности, инструкции или политики безопасности. 



## Архитектура 

### V1.7 Ошибки, логирование и аудит

**Средние и высокие требования:**

1. В системе используется общий формат и подход к логированию.
2. Логи безопасно передаются в, предпочтительно, удаленную систему для анализа, обнаружения, оповещения и эскалации. 

### V1.8 Приватность и защита данных

**Средние и высокие требования:**

1. Все конфиденциальные данные идентифицированы и классифицированы по уровням защиты. 
2. Все уровни защиты имеют взаимосвязанные требования защиты, например, требования шифрования, целостности, сохранения, приватности и иных требований конфиденциальности и приватности и эти требования применены в архитектуре. 

### V1.9 Коммуникации

**Средние и высокие требования:**

1. Приложение шифрует коммуникации между компонентами, в частности, когда эти компоненты находятся в разных контейнерах, системах, сайтах или в разных облачных сервисах. 
2. Компоненты приложения проверяют подлинность каждой стороны коммуникации, чтобы предотвратить men-in-the-middle атаку. Например, компоненты приложения должны валидировать TLS сертификаты и цепочки доверия. 

### V1.10 Вредоносное ПО

**Средние и высокие требования:**

1. Используется система контроля исходного кода, в ней можно создать тикеты о проблемах и изменениях. В этой системе используется контроль доступа и отслеживаются любые изменения идентифицированных пользователей. 

### V1.11 Бизнес логика 

**Средние требования:** 

1. Определены и описаны все бизнес функции и функции безопасности компонентов приложения. 
2. Синхронизирвоаны все ценные бизнес процессы, включая аутентификацию, управление сессиями и контроль доступа. 

**Только высокие требования:** 

1. Все бизнес процессы, включая аутентификацию, управление сессиями, управление доступом устойчивы к атакам "time-of-check" и "time-of-use race conditions"

### \*V11.1 Безопасность бизнес-логики

**Низкие, средние и высокие требования:**

1. Приложение исполняет шаги бизнес логики для пользователя последовательно и без пропуска шагов. 
2. Приложение исполняет каждый шаг бизнес логики в реалистичное время для человека, другими словами, транзакции не проводятся слишком быстро. 
3. Приложение имеет лимиты для отдельных бизнес процессов или транзакций, которые выполняются для каждого пользователя отдельно. 
4. В приложении реализованы лимиты для обнаружения и защиты от автоматизированных атак по типу фильтрации данных, чрезмерного обращения к процессам бизнес логики, чрезмерной загрузки файлов или DOS \(отказ в обслуживании\)
5. * Приложение имеет лимиты для бизнес логики или валидации для защиты от возможных бизнес-рисков или угроз, выявленных с помощью моделирования угроз или похожих методик. 

**Только средние и высокие требования:**

1. Приложение не испытывает проблем с "time of check to time of use" \(TOCTOU\) и других проблем с важными процессами в состоянии гонки. 
2. Приложение отслеживает необычные события или активность с точки зрения бизнес-логики. Например, попытки совершить действия не по порядку или действия, которые обычный пользователь никогда бы не предпринял. 
3. Приложение имеет настраиваемую систему оповещения об обнаружении автоматизированных атаках или необычной активности. 

### V14.1 Сборка

**Средние и высокие требования:**

1. Процессы сборки и развертывания приложения производятся безопасно, например, произведена автоматизация CI /CD, автоматизированы конфигурации и существуют скрипты автоматического развертывания. 
2. Флаги компилятора настроены таким образом, чтобы обеспечить безопасную сборку \(включение всех доступных оповещений о переполнении буфера, рандомизация стека, предотвращение исполнения данных, остановка сборки если найдены небезопасные операции с указателями, памятью, форматированием строк\)
3. Конфигурация сервера настроена в соответствии с рекомендациями приложения сервера и используемых фреймворков. 
4. Приложение, конфигурации и все зависимости могут быть развернуты при помощи скриптов, составленных из документированных и протестированных последовательностей команд в разумные сроки или они могут быть восстановлены из резервных копий своевременно. 

**Только высокие требования:**

1. Авторизованные администраторы могут проверить целостность всех важных с точки зрения безопасности конфигураций для определения вмешательства в них. 

### V14.2 Зависимости

**Низкие, средние и высокие требования:**

1. Все компоненты обновлены. Во время сборки или компиляции используется dependency checker для проверки версий библиотек. 
2. Все неиспользуемые функции, документация, примеры и конфигурации удалены, например, тестовые приложения, документация платформы или пользователи по умолчанию и временные пользователи для тестов. 
3. Если элементы приложения, такие как библиотеки JavaScript, таблицы стилей CSS или шрифты хранятся во внешней сети доставки контента \(CDN\) или у внешнего провайдера, то используются средства проверки целостности ресурсов \(Subresource Integrity или SRI\). 

**Только средние и высокие требования:**

1. Все сторонние компоненты поставляются от определенных, доверенных и постоянно обновляемых репозиториев. 
2. Существует перечень всех используемых сторонних библиотек. 
3. Сторонние библиотеки работают из песочницы или через wrapper'ы, чтобы добиться только требуемого от них поведения в приложении для уменьшения поверхности атаки.

### V14.3 Непреднамеренное раскрытие информации

**Низкие, средние и высокие требования:**

1. Сообщения об ошибках фреймворка, веб и серверных приложений настроены и доставляют пользователю актуальные, персонализированные ответы для избежания непреднамеренного раскрытия конфиденциальной и иной критичной с точки зрения безопасности системной информации.   
2. Отладочные режимы фреймворка, веб и серверных приложений отключены в рабочем окружении, чтобы опции отладки, консоли разработчика были отключены во избежание непреднамеренного раскрытия конфиденциальной и иной критичной с точки зрения безопасности системной информации.   
3. Заголовки или иные части HTTP ответа не раскрывают детальную информацию о компонентах системы и информацию о версиях.  

## Backend 

### \*V1.2 Аутентификация

**Средние и высокие требования:**

1. Во всех приложениях, компонентах, сервисах и на всех серверах используются уникальные или специальных низкопривилегированные учетные записи операционной системы
2. Используется аутентификация в коммуникациях между компонентами приложений, включая API, промежуточное ПО и уровни данных. Компоненты должны иметь привилегии не выше необходимого минимума. 
3. \*Приложение использует единый проверенный и безопасный механизм аутентификации, он может быть расширен для использования строгой аутентификации, имеет подробное логирование для обнаружения зловредных действий с аккаунтов. 
4. \*Все пути аутентификации и API контроля идентификации производят последовательный контроль безопасности аутентификации и нет иных небезопасных альтернатив для аутентификации. 

### V1.4 Управление доступом

**Средние и высокие требования:**

1. Все точки управления доступом, такие как шлюзы управления доступом, серверы, бессерверные функции обеспечивают контроль доступа. Управление доступом не производится на стороне клиента. 
2. Выбранное решение для управления доступом достаточно гибкое, чтобы обеспечить нужды приложения. 
3. Для всех функций, данных, URL адресов, контроллеров, сервисов и других ресурсов применяется принцип минимально необходимых привилегий. 
4. Приложение использует единственный и хорошо проверенный механизм контроля доступа для обращения к защищенным данным и ресурсам. Все запросы должны передаваться через этот единый механизм. 
5. Контроль доступа использует атрибут или функцию, которая проверяет, есть ли у данного авторизованного пользователя доступ к функции / данным, а не просто проверяет его роль. Разрешения все же должны выдаваться на основе ролей. 

### V1.5 Ввод и вывод

**Средние и высокие требования:**

1. Требования к вводу и выводу четко определяют как обрабатывать данные на основе типа, контента, применяемых законов, нормативов и других политик.  
2. Сериализация не используется в коммуникации с недоверенными клиентами. Если это невозможно, то для предотвращения атак десериализации и инъекции объектов применяются средства контроля целостности \(и шифрование, если отправляются конфиденциальные данные\). 
3. Проверка ввода используется на доверенном сервисном уровне. 
4. Убедитесь, что кодировка вывода происходит рядом с интерпретатором, для которого она предназначена, или с помощью этого интерпретатора. 

### V1.6 Криптография

**Средние и высокие требования:**

1. Существует четкая политика управления криптографическими ключами и жизненный цикл криптографического ключа соответствует стандарту управления ключами, например NIST SP 800-57.
2. Пользователи криптографических сервисов защищают конфиденциальные данные и другие секреты с помощью хранилищ ключей или альтернатив на основе API.
3. Все ключи и пароли заменяемы, работают через четко определенный процесс для возможности повторного шифрования конфиденциальных данных при смене ключа / пароля.
4. Все ключи, пароли или секреты API, сгенерированные при помощи симметричных алгоритмов, генерируемые клиентами или предоставляемые им, используются только для защиты секретов с низким уровнем риска, например, при шифровании локального хранилища, для временного использования, как, например, обфусация параметров. Обмен секретами с клиентами производится эквивалентно чистому тексту с архитектурной точки зрения. 

### V1.12 Безопасная загрузка файлов

**Средние и высокие требования:**

1. Загружаемые пользователями файлы хранятся вне директории веб-приложения. 
2. Загруженные пользователями файлы, если требуется их отображение или загрузка через приложение, обрабатываются через MIME-тип `application/octet-stream` или через внешний домен, как, например, облачное хранилище. Реализована подходящая политика безопасности контента, чтобы снизить риск от XSS-векторов или других атак со стороны загруженного файла.

### V1.14 Конфигурация

**Средние и высокие требования:**

1. Компоненты разделены на разные уровни доверия через четко определенную схему контроля безопасности, правила брандмауэра, API-шлюзы, обратные прокси, облачные группы безопасности или похожие механизмы. 
2. При развертывании исполняемых файлов на недоверенных устройствах используются подписи, доверенные соединения и проверенные конечные точки. 
3. Пайплайны предупреждают об устаревших и небезопасных компонентах при сборке и при необходимости прерывают сборку. 
4. Пайплайн содержит этап сборки для автоматической сборки и подтверждения безопасного развертывания приложения, особенно если инфраструктура приложения определяется кодом \(Software-defined infrastructure или SDI\), например, скрипты сборки облачного окружения.
5. Развертывание приложения изолировано, контейнеризовано на сетевом уровне, чтобы осложнить и задержать атаку из других приложений, особенно, если атакующие производят десериализацию.
6. Приложение не использует неподдерживаемые, небезопасные или устаревшие технологии на стороне клиента, например плагины NSAPI, Flash, Shockwave, ActiveX, Silverlight, NACL, или Java апплеты на стороне клиента.

### V2.2 Общие требования к аутентификатору

**Низкие, средние и высокие требования:**

1. Уведомления безопасности отправляются пользователям после обновлений в части аутентификации, например, при смене учетных данных, вход из неизвестных или опасных локаций. Предпочтительно использование PUSH-уведомлений вместо SMS или уведомлений по электронной почте, а в случае отсутствия возможности отправлять PUSH-уведомления, SMS или email-уведомления не должны содержать конфиденциальной информации. 

**Только высокие требования::** 

1. Используется защита от выдачи атакующего за клиента вследствие фишинг атак, например, через многофакторную аутентификацию, использование крипторафических устройств с подтверждением \(например, привязанные ключи, требующие нажатия для аутентификации\) или через аутентификацию на высших уровнях ALL \(Authenticator Assurance Level\), сертификаты на стороне клиента. 
2. Поставщик учетных данных \(credential service provider или CSP\) и приложение, проверяющее подлинность аутентификации, разделены и между ними находится аутентифицированный обеими сторонами TLS. 
3. Реализована защита от атаки повторного воспроизведения через использование OTP-устройств, криптографических аутентификаторов или кодов подтверждения. 
4. При попытке аутентификации, приложение требует ввода OTP-токена или действия, заданного пользователем, например, нажатия кнопки на ключе FIDO. 

### V2.3 Жизненный цикл аутентификатора

**Низкие, средние и высокие требования:** 

1. Сгенерированные системой начальные пароли или коды активации создаются с помощью генератора случайных чисел, должны содержать не менее 6 символов, могут содержать буквы и цифры, истекать через короткий период времени. Эти начальные секреты не используются в долгосрочной перспективе. 

**Только средние и высокие требования:**

1. Поддерживается регистрация и использование выбранных пользователями устройств аутентификации, как, например токены U2F или FIDO. 
2. При приближении окончания срока действия аутентификатора, инструкции по обновлению отправляются пользователю с учетом достаточного времени для прохождения процедуры обновления. 

### \*V2.4 Хранение учетных данных 

**Средние и высокие требования:**

1. \*Пароли хранятся в форме, устойчивой к офлайн атакам. Пароли должны быть хешированы с добавлением "соли" с использованием утвержденной функции шифрования ключа или функции хеширования пароля. Эти функции берут пароль, соль и фактор стоимости на вход, когда генерируют хэш пароля. 
2. Соль содержит в себе не менее 32 битов и была создана рандомно для минимизации возможности повторного использования этой соли среди хранимых хешей. Для каждого набора учетных данных хранится уникальное значение соли и сгенерированный хэш. 
3. Если используется PBKDF2, количество итераций должно быть велико настолько, насколько позволяет производительность верификационного сервера, что часто составляет 100 000 итераций. 
4. Если используется bcrypt, фактор работы должен быть высоким настолько, насколько это позволяет производительность сервера, что часто составляет минимум 13 единиц. 
5. Используется дополнительная итерация функции формирования ключа, где значение соли хранится в секрете и доступно только верификатору. Значение соли генерируется с использованием генератора рандомного бита \[SP 800-90Ar1\], при этом 
6. 7. Verify that an additional iteration of a key derivation function is performed, using a salt value that is secret and known only to the verifier. Generate the salt value using an approved random bit generator \[SP 800-90Ar1\] and provide at least the minimum security strength specified in the latest revision of SP 800-131A. The secret salt value SHALL be stored separately from the hashed passwords \(e.g., in a specialized device like a hardware security module\).

### V2.5 Credential Recovery Requirements

**Low, medium and high requirements:** 

1. Verify that a system generated initial activation or recovery secret is not sent in clear text to the user.
2. Verify password hints or knowledge-based authentication \(so-called "secret questions"\) are not present.
3. Verify password credential recovery does not reveal the current password in any way.
4. Verify shared or default accounts are not present \(e.g. "root", "admin", or "sa"\).
5. Verify that if an authentication factor is changed or replaced, that the user is notified of this event.
6. Verify forgotten password, and other recovery paths use a secure recovery mechanism, such as TOTP or other soft token, mobile push, or another offline recovery mechanism.

**Medium and high requirements only:** 

1. Verify that if OTP or multi-factor authentication factors are lost, that evidence of identity proofing is performed at the same level as during enrollment.

### V2.6 Look-up Secret Verifier Requirements

**Medium and high requirements:** 

1. Verify that lookup secrets can be used only once.
2. Verify that lookup secrets have sufficient randomness \(112 bits of entropy\), or if less than 112 bits of entropy, salted with a unique and random 32-bit salt and hashed with an approved one-way hash.
3. Verify that lookup secrets are resistant to offline attacks, such as predictable values.

### V2.7 Out of Band Verifier Requirements

**Low, medium and high requirements:** 

1. Verify that clear text out of band \(NIST "restricted"\) authenticators, such as SMS or PSTN, are not offered by default, and stronger alternatives such as push notifications are offered first.
2. Verify that the out of band verifier expires out of band authentication requests, codes, or tokens after 10 minutes.
3. Verify that the out of band verifier authentication requests, codes, or tokens are only usable once, and only for the original authentication request.
4. Verify that the out of ban
5. d authenticator and verifier communicates over a secure independent channel.

**Medium and high requirements only:** 

1. Verify that the out of band verifier retains only a hashed version of the authentication code.
2. Verify that the initial authentication code is generated by a secure random number generator, containing at least 20 bits of entropy \(typically a six digital random number is sufficient\).

### V2.8 Single or Multi Factor One Time Verifier Requirements

**Low, medium and high requirements:** 

1. Verify that time-based OTPs have a defined lifetime before expiring.

**Medium and high requirements only:** 

1. Verify that symmetric keys used to verify submitted OTPs are highly protected, such as by using a hardware security module or secure operating system based key storage.
2. Verify that approved cryptographic algorithms are used in the generation, seeding, and verification.
3. Verify that time-based OTP can be used only once within the validity period.
4. Verify that if a time-based multi factor OTP token is re-used during the validity period, it is logged and rejected with secure notifications being sent to the holder of the device.
5. Verify physical single factor OTP generator can be revoked in case of theft or other loss. Ensure that revocation is immediately effective across logged in sessions, regardless of location.
6. Verify that biometric authenticators are limited to use only as secondary factors in conjunction with either something you have and something you know.

### V2.9 Cryptographic Software and Devices Verifier Requirements

**Medium and high requirements:**

1. Verify that cryptographic keys used in verification are stored securely and protected against disclosure, such as using a TPM or HSM, or an OS service that can use this secure storage.
2. Verify that the challenge nonce is at least 64 bits in length, and statistically unique or unique over the lifetime of the cryptographic device.
3. Verify that approved cryptographic algorithms are used in the generation, seeding, and verification.

### V2.10 Service Authentication Requirements

**Medium and high requirements:** 

1. Verify that integration secrets do not rely on unchanging passwords, such as API keys or shared privileged accounts.
2. Verify that if passwords are required, the credentials are not a default account.
3. Verify that passwords are stored with sufficient protection to prevent offline recovery attacks, including local system access.
4. Verify passwords, integrations with databases and third-party systems, seeds and internal secrets, and API keys are managed securely and not included in the source code or stored within source code repositories. Such storage SHOULD resist offline attacks. The use of a secure software key store \(L1\), hardware trusted platform module \(TPM\), or a hardware security module \(L3\) is recommended for password storage.

### V3.1 Fundamental Session Management Requirements

**Low, medium and high requirements:** 

1. Verify the application never reveals session tokens in URL parameters or error messages.

### V3.2 Session Binding Requirements

**Low, medium and high requirements:** 

1. Verify the application generates a new session token on user authentication.
2. Verify that session tokens possess at least 64 bits of entropy.
3. Verify the application only stores session tokens in the browser using secure methods such as appropriately secured cookies \(see section 3.4\) or HTML 5 session storage.

 **Medium and high requirements only:** 

1. Verify that session token are generated using approved cryptographic algorithms.

### V3.3 Session Logout and Timeout Requirements

**Low, medium and high requirements:** 

1. Verify that logout and expiration invalidate the session token, such that the back button or a downstream relying party does not resume an authenticated session, including across relying parties.
2. If authenticators permit users to remain logged in, verify that re-authentication occurs periodically both when actively used or after an idle period.

**Medium and high requirements only:** 

1. Verify that the application terminates all other active sessions after a successful password change, and that this is effective across the application, federated login \(if present\), and any relying parties.
2. Verify that users are able to view and log out of any or all currently active sessions and devices.

### V3.5 Token-based Session Management

**Medium and high requirements only:** 

1. Verify the application does not treat OAuth and refresh tokens — on their own — as the presence of the subscriber and allows users to terminate trust relationships with linked applications.
2. Verify the application uses session tokens rather than static API secrets and keys, except with legacy implementations.
3. Verify that stateless session tokens use digital signatures, encryption, and other countermeasures to protect against tampering, enveloping, replay, null cipher, and key substitution attacks.

### V3.6 Re-authentication from a Federation or Assertion

**High requirements only:**

1. Verify that relying parties specify the maximum authentication time to CSPs and that CSPs re-authenticate the subscriber if they haven't used a session within that period.
2. Verify that CSPs inform relying parties of the last authentication event, to allow RPs to determine if they need to re-authenticate the user.

### V3.7 Defenses Against Session Management Exploits

**Low, medium and high requirements:** 

1. Verify the application ensures a valid login session or requires reauthentication or secondary verification before allowing any sensitive transactions or account modifications.

### V4.1 General Access Control Design

**Low, medium and high requirements:** 

1. Verify that the application enforces access control rules on a trusted service layer, especially if client-side access control is present and could be bypassed.
2. Verify that all user and data attributes and policy information used by access controls cannot be manipulated by end users unless specifically authorized.
3. Verify that the principle of least privilege exists - users should only be able to access functions, data files, URLs, controllers, services, and other resources, for which they possess specific authorization. This implies protection against spoofing and elevation of privilege.
4. Verify that the principle of deny by default exists whereby new users/roles start with minimal or no permissions and users/roles do not receive access to new features until access is explicitly assigned.
5. Verify that access controls fail securely including when an exception occurs.

### V5.2 Sanitization and Sandboxing Requirements

**Low, medium and high requirements:**

1. Verify that all untrusted HTML input from WYSIWYG editors or similar is properly sanitized with an HTML sanitizer library or framework feature.
2. Verify that unstructured data is sanitized to enforce safety measures such as allowed characters and length.
3. Verify that the application sanitizes user input before passing to mail systems to protect against SMTP or IMAP injection.
4. Verify that the application avoids the use of eval\(\) or other dynamic code execution features. Where there is no alternative, any user input being included must be sanitized or sandboxed before being executed.
5. Verify that the application protects against template injection attacks by ensuring that any user input being included is sanitized or sandboxed.
6. Verify that the application protects against SSRF attacks, by validating or sanitizing untrusted data or HTTP file metadata, such as filenames and URL input fields, use whitelisting of protocols, domains, paths and ports.
7. Verify that the application sanitizes, disables, or sandboxes user-supplied SVG scriptable content, especially as they relate to XSS resulting from inline scripts, and foreignObject.
8. Verify that the application sanitizes, disables, or sandboxes user-supplied scriptable or expression template language content, such as Markdown, CSS or XSL stylesheets, BBCode, or similar.

### V5.3 Output encoding and Injection Prevention Requirements

**Low, medium and high requirements:**

1. Verify that output encoding is relevant for the interpreter and context required. For example, use encoders specifically for HTML values, HTML attributes, JavaScript, URL Parameters, HTTP headers, SMTP, and others as the context requires, especially from untrusted inputs \(e.g. names with Unicode or apostrophes, such as ねこ or O'Hara\).
2. Verify that output encoding preserves the user's chosen character set and locale, such that any Unicode character point is valid and safely handled.
3. Verify that context-aware, preferably automated - or at worst, manual - output escaping protects against reflected, stored, and DOM based XSS.
4. Verify that data selection or database queries \(e.g. SQL, HQL, ORM, NoSQL\) use parameterized queries, ORMs, entity frameworks, or are otherwise protected from database injection attacks.
5. Verify that where parameterized or safer mechanisms are not present, contextspecific output encoding is used to protect against injection attacks, such as the use of SQL escaping to protect against SQL injection.
6. Verify that the application projects against JavaScript or JSON injection attacks, including for eval attacks, remote JavaScript includes, CSP bypasses, DOM XSS, and JavaScript expression evaluation.
7. Verify that the application protects against LDAP Injection vulnerabilities, or that specific security controls to prevent LDAP Injection have been implemented.
8. Verify that the application protects against OS command injection and that operating system calls use parameterized OS queries or use contextual command line output encoding.
9. Verify that the application protects against Local File Inclusion \(LFI\) or Remote File Inclusion \(RFI\) attacks.
10. Verify that the application protects against XPath injection or XML injection attacks.

### V5.4 Memory, String, and Unmanaged Code Requirements

**Medium and high requirements:**

1. Verify that the application uses memory-safe string, safer memory copy and pointer arithmetic to detect or prevent stack, buffer, or heap overflows.
2. Verify that format strings do not take potentially hostile input, and are constant.
3. Verify that sign, range, and input validation techniques are used to prevent integer overflows.

### V5.5 Deserialization Prevention Requirements

**Low, medium and high requirements:**

1. Verify that serialized objects use integrity checks or are encrypted to prevent hostile object creation or data tampering.
2. Verify that the application correctly restricts XML parsers to only use the most restrictive configuration possible and to ensure that unsafe features such as resolving external entities are disabled to prevent XXE.
3. Verify that deserialization of untrusted data is avoided or is protected in both custom code and third-party libraries \(such as JSON, XML and YAML parsers\).
4. Verify that when parsing JSON in browsers or JavaScript-based backends, JSON.parse is used to parse the JSON document. Do not use eval\(\) to parse JSON.

### V6.1 Data Classification

**Medium and high requirements:**

1. Verify that regulated private data is stored encrypted while at rest, such as personally identifiable information \(PII\), sensitive personal information, or data assessed likely to be subject to EU's GDPR.
2. Verify that regulated health data is stored encrypted while at rest, such as medical records, medical device details, or de-anonymized research records.
3. Verify that regulated financial data is stored encrypted while at rest, such as financial accounts, defaults or credit history, tax records, pay history, beneficiaries, or de-anonymized market or research records.

### V6.2 Algorithms

**Low, medium and high requirements:**

1. Verify that all cryptographic modules fail securely, and errors are handled in a way that does not enable Padding Oracle attacks.

**Medium and high requirements only:**

1. Verify that industry proven or government approved cryptographic algorithms, modes, and libraries are used, instead of custom coded cryptography.
2. Verify that encryption initialization vector, cipher configuration, and block modes are configured securely using the latest advice.
3. Verify that random number, encryption or hashing algorithms, key lengths, rounds, ciphers or modes, can be reconfigured, upgraded, or swapped at any time, to protect against cryptographic breaks.
4. Verify that known insecure block modes \(i.e. ECB, etc.\), padding modes \(i.e. PKCS\#1 v1.5, etc.\), ciphers with small block sizes \(i.e. Triple-DES, Blowfish, etc.\), and weak hashing algorithms \(i.e. MD5, SHA1, etc.\) are not used unless required for backwards compatibility.
5. Verify that nonces, initialization vectors, and other single use numbers must not be used more than once with a given encryption key. The method of generation must be appropriate for the algorithm being used.

**High requirements only:**

1. Verify that encrypted data is authenticated via signatures, authenticated cipher modes, or HMAC to ensure that ciphertext is not altered by an unauthorized party.
2. Verify that all cryptographic operations are constant-time, with no 'short-circuit' operations in comparisons, calculations, or returns, to avoid leaking information.

### V6.3 Random Values

**Medium and high requirements:**

1. Verify that all random numbers, random file names, random GUIDs, and random strings are generated using the cryptographic module's approved cryptographically secure random number generator when these random values are intended to be not guessable by an attacker.
2. Verify that random GUIDs are created using the GUID v4 algorithm, and a cryptographically-secure pseudo-random number generator \(CSPRNG\). GUIDs created using other pseudo-random number generators may be predictable.

**High requirements only:** 

1. Verify that random numbers are created with proper entropy even when the application is under heavy load, or that the application degrades gracefully in such circumstances. 

### V6.4 Secret Management

**Medium and high requirements:**

1. Verify that a secrets management solution such as a key vault is used to securely create, store, control access to and destroy secrets.
2. Verify that key material is not exposed to the application but instead uses an isolated security module like a vault for cryptographic operations.

### V7.1 Log Content Requirements

**Low, medium and high requirements:**

1. Verify that the application does not log credentials or payment details. Session tokens should only be stored in logs in an irreversible, hashed form.
2. Verify that the application does not log other sensitive data as defined under local privacy laws or relevant security policy.

**Medium and high requirements only:**

1. Verify that the application logs security relevant events including successful and failed authentication events, access control failures, deserialization failures and input validation failures.
2. Verify that each log event includes necessary information that would allow for a detailed investigation of the timeline when an event happens. 

### V7.2 Log Processing Requirements

**Medium and high requirements:**

1. Verify that all authentication decisions are logged, without storing sensitive session identifiers or passwords. This should include requests with relevant metadata needed for security investigations.
2. Verify that all access control decisions can be logged and all failed decisions are logged. This should include requests with relevant metadata needed for security investigations.

### V7.3 Log Protection Requirements

**Medium and high requirements:**

1. Verify that the application appropriately encodes user-supplied data to prevent log injection.
2. Verify that all events are protected from injection when viewed in log viewing software.
3. Verify that security logs are protected from unauthorized access and modification.
4. Verify that time sources are synchronized to the correct time and time zone. Strongly consider logging only in UTC if systems are global to assist with postincident forensic analysis.

### V7.4 Error Handling

**Low, medium and high requirements:**

1. Verify that a generic message is shown when an unexpected or security sensitive error occurs, potentially with a unique ID which support personnel can use to investigate.

**Medium and high requirements only:**

1. Verify that exception handling \(or a functional equivalent\) is used across the codebase to account for expected and unexpected error conditions.
2. Verify that a "last resort" error handler is defined which will catch all unhandled exceptions.

### V8.1 General Data Protection

**Medium and high requirements:**

1. Verify the application protects sensitive data from being cached in server components such as load balancers and application caches.
2. Verify that all cached or temporary copies of sensitive data stored on the server are protected from unauthorized access or purged/invalidated after the authorized user accesses the sensitive data.
3. Verify the application minimizes the number of parameters in a request, such as hidden fields, Ajax variables, cookies and header values.
4. Verify the application can detect and alert on abnormal numbers of requests, such as by IP, user, total per hour or day, or whatever makes sense for the application.

**High requirements only:**

1. Verify that regular backups of important data are performed and that test restoration of data is performed.
2. Verify that backups are stored securely to prevent data from being stolen or corrupted.



### V8.3 Sensitive Private Data

**Low, medium and high requirements:**

1. Verify that all sensitive data created and processed by the application has been identified, and ensure that a policy is in place on how to deal with sensitive data.

**Medium and high requirements only:**

1. Verify accessing sensitive data is audited \(without logging the sensitive data itself\), if the data is collected under relevant data protection directives or where logging of access is required.
2. Verify that sensitive information contained in memory is overwritten as soon as it is no longer required to mitigate memory dumping attacks, using zeroes or random data.
3. Verify that sensitive or private information that is required to be encrypted, is encrypted using approved algorithms that provide both confidentiality and integrity.
4. Verify that sensitive personal information is subject to data retention classification, such that old or out of date data is deleted automatically, on a schedule, or as the situation requires.

### V9.1 Communications Security Requirements

**Low, medium and high requirements:**

1. Verify that secured TLS is used for all client connectivity, and does not fall back to insecure or unencrypted protocols.
2. Verify using online or up to date TLS testing tools that only strong algorithms, ciphers, and protocols are enabled, with the strongest algorithms and ciphers set as preferred.
3. Verify that old versions of SSL and TLS protocols, algorithms, ciphers, and configuration are disabled, such as SSLv2, SSLv3, or TLS 1.0 and TLS 1.1. The latest version of TLS should be the preferred cipher suite.

### V9.2 Server Communications Security Requirements

**Medium and high requirements:**

1. Verify that connections to and from the server use trusted TLS certificates. Where internally generated or self-signed certificates are used, the server must be configured to only trust specific internal CAs and specific self-signed certificates. All others should be rejected.
2. Verify that encrypted communications such as TLS is used for all inbound and outbound connections, including for management ports, monitoring, authentication, API, or web service calls, database, cloud, serverless, mainframe, external, and partner connections. The server must not fall back to insecure or unencrypted protocols.
3. Verify that all encrypted connections to external systems that involve sensitive information or functions are authenticated.
4. Verify that proper certification revocation, such as Online Certificate Status Protocol \(OCSP\) Stapling, is enabled and configured.

**High requirements only:**

1. Verify that backend TLS connection failures are logged.

### V10.1 Code Integrity Controls

**High requirements only:**

1. Verify that a code analysis tool is in use that can detect potentially malicious code, such as time functions, unsafe file operations and network connections.

### V10.2 Malicious Code Search

**Medium and high requirements:**

1. Verify that the application source code and third party libraries do not contain unauthorized phone home or data collection capabilities. Where such functionality exists, obtain the user's permission for it to operate before collecting any data.
2. Verify that the application does not ask for unnecessary or excessive permissions to privacy related features or sensors, such as contacts, cameras, microphones, or location.

**High requirements only:**

1. Verify that the application source code and third party libraries do not contain back doors, such as hard-coded or additional undocumented accounts or keys, code obfuscation, undocumented binary blobs, rootkits, or anti-debugging, insecure debugging features, or otherwise out of date, insecure, or hidden functionality that could be used maliciously if discovered.
2. Verify that the application source code and third party libraries does not contain time bombs by searching for date and time related functions.
3. Verify that the application source code and third party libraries does not contain malicious code, such as salami attacks, logic bypasses, or logic bombs.
4. Verify that the application source code and third party libraries do not contain Easter eggs or any other potentially unwanted functionality.

### V10.3 Deployed Application Integrity Controls

**Low, medium and high requirements:**

1. Verify that if the application has a client or server auto-update feature, updates should be obtained over secure channels and digitally signed. The update code must validate the digital signature of the update before installing or executing the update.
2. Verify that the application employs integrity protections, such as code signing or sub-resource integrity. The application must not load or execute code from untrusted sources, such as loading includes, modules, plugins, code, or libraries from untrusted sources or the Internet.
3. Verify that the application has protection from sub-domain takeovers if the application relies upon DNS entries or DNS sub-domains, such as expired domain names, out of date DNS pointers or CNAMEs, expired projects at public source code repos, or transient cloud APIs, serverless functions, or storage buckets \(autogen-bucket-id.cloud.example.com\) or similar. Protections can include ensuring that DNS names used by applications are regularly checked for expiry or change.

### V12.1 File Upload Requirements

**Low, medium and high requirements:**

1. Verify that the application will not accept large files that could fill up storage or cause a denial of service attack.

**Medium and high requirements only:**

1. Verify that compressed files are checked for "zip bombs" - small input files that will decompress into huge files thus exhausting file storage limits.
2. Verify that a file size quota and maximum number of files per user is enforced to ensure that a single user cannot fill up the storage with too many files, or excessively large files.

### V12.2 File Integrity Requirements

**Medium and high requirements:**

1. Verify that files obtained from untrusted sources are validated to be of expected type based on the file's content.

### V12.3 File execution Requirements

**Low, medium and high requirements:**

1. Verify that user-submitted filename metadata is not used directly with system or framework file and URL API to protect against path traversal.
2. Verify that user-submitted filename metadata is validated or ignored to prevent the disclosure, creation, updating or removal of local files \(LFI\).
3. Verify that user-submitted filename metadata is validated or ignored to prevent the disclosure or execution of remote files \(RFI\), which may also lead to SSRF.
4. Verify that the application protects against reflective file download \(RFD\) by validating or ignoring user-submitted filenames in a JSON, JSONP, or URL parameter, the response Content-Type header should be set to text/plain, and the Content-Disposition header should have a fixed filename.
5. Verify that untrusted file metadata is not used directly with system API or libraries, to protect against OS command injection.

**Medium and high requirements only:**

1. Verify that the application does not include and execute functionality from untrusted sources, such as unverified content distribution networks, JavaScript libraries, node npm libraries, or server-side DLLs.

### V12.4 File Storage Requirements

**Low, medium and high requirements:**

1. Verify that files obtained from untrusted sources are stored outside the web root, with limited permissions, preferably with strong validation.
2. Verify that files obtained from untrusted sources are scanned by antivirus scanners to prevent upload of known malicious content.

### V12.6 SSRF Protection Requirements

**Low, medium and high requirements:**

1. Verify that the web or application server is configured with a whitelist of resources or systems to which the server can send requests or load data/files from.

### V13.1 Generic Web Service Security Verification Requirements

**Low, medium and high requirements:**

1. Verify that all application components use the same encodings and parsers to avoid parsing attacks that exploit different URI or file parsing behavior that could be used in SSRF and RFI attacks.
2. Verify that access to administration and management functions is limited to authorized administrators.
3. Verify API URLs do not expose sensitive information, such as the API key, session tokens etc.

**Medium and high requirements only:**

1. Verify that authorization decisions are made at both the URI, enforced by programmatic or declarative security at the controller or router, and at the resource level, enforced by model-based permissions.
2. Verify that requests containing unexpected or missing content types are rejected with appropriate headers \(HTTP response status 406 Unacceptable or 415 Unsupported Media Type\).

### V13.2 RESTful Web Service Verification Requirements

**Low, medium and high requirements:**

1. Verify that enabled RESTful HTTP methods are a valid choice for the user or action, such as preventing normal users using DELETE or PUT on protected API or resources.
2. Verify that JSON schema validation is in place and verified before accepting input.
3. Verify that RESTful web services that utilize cookies are protected from CrossSite Request Forgery via the use of at least one or more of the following: triple or double submit cookie pattern \(see references\), CSRF nonces, or ORIGIN request header checks.

**Medium and high requirements only:**

1. Verify that REST services have anti-automation controls to protect against excessive calls, especially if the API is unauthenticated.
2. Verify that REST services explicitly check the incoming Content-Type to be the expected one, such as application/xml or application/JSON.
3. Verify that the message headers and payload are trustworthy and not modified in transit. Requiring strong encryption for transport \(TLS only\) may be sufficient in many cases as it provides both confidentiality and integrity protection. Permessage digital signatures can provide additional assurance on top of the transport protections for high-security applications but bring with them additional complexity and risks to weigh against the benefits.

### V13.4 GraphQL and other Web Service Data Layer Security Requirements

**Medium and high requirements:**

1. Verify that query whitelisting or a combination of depth limiting and amount limiting should be used to prevent GraphQL or data layer expression denial of service \(DoS\) as a result of expensive, nested queries. For more advanced scenarios, query cost analysis should be used.
2. Verify that GraphQL or other data layer authorization logic should be implemented at the business logic layer instead of the GraphQL layer.

### V14.4 HTTP Security Headers Requirements

**Low, medium and high requirements:**

1. Verify that every HTTP response contains a content type header specifying a safe character set \(e.g., UTF-8, ISO 8859-1\).
2. Verify that all API responses contain Content-Disposition: attachment; filename="api.json" \(or other appropriate filename for the content type\).
3. Verify that a content security policy \(CSPv2\) is in place that helps mitigate impact for XSS attacks like HTML, DOM, JSON, and JavaScript injection vulnerabilities.
4. Verify that all responses contain X-Content-Type-Options: nosniff.
5. Verify that HTTP Strict Transport Security headers are included on all responses and for all subdomains, such as Strict-Transport-Security: max-age=15724800; includeSubdomains.
6. Verify that a suitable "Referrer-Policy" header is included, such as "no-referrer" or "same-origin".
7. Verify that a suitable X-Frame-Options or Content-Security-Policy: frameancestors header is in use for sites where content should not be embedded in a third-party site.

### V14.5 Validate HTTP Request Header Requirements

**Low, medium and high requirements:**

1. Verify that the application server only accepts the HTTP methods in use by the application or API, including pre-flight OPTIONS.
2. Verify that the supplied Origin header is not used for authentication or access control decisions, as the Origin header can easily be changed by an attacker.
3. Verify that the cross-domain resource sharing \(CORS\) Access-Control-AllowOrigin header uses a strict white-list of trusted domains to match against and does not support the "null" origin.

**Medium and high requirements only:**

1. Verify that HTTP headers added by a trusted proxy or SSO devices, such as a bearer token, are authenticated by the application.

## Frontend

### V2.1 Password Security Requirements

**Low, medium and hard requirements:** 

1. Verify that user set passwords are at least 12 characters in length.
2. Verify that passwords 64 characters or longer are permitted.
3. Verify that passwords can contain spaces and truncation is not performed. Consecutive multiple spaces MAY optionally be coalesced.
4. Verify that Unicode characters are permitted in passwords. A single Unicode code point is considered a character, so 12 emoji or 64 kanji characters should be valid and permitted.
5. Verify users can change their password.
6. Verify that password change functionality requires the user's current and new password.
7. Verify that passwords submitted during account registration, login, and password change are checked against a set of breached passwords either locally \(such as the top 1,000 or 10,000 most common passwords which match the system's password policy\) or using an external API. If using an API a zero knowledge proof or other mechanism should be used to ensure that the plain text password is not sent or used in verifying the breach status of the password. If the password is breached, the application must require the user to set a new nonbreached password.
8. Verify that a password strength meter is provided to help users set a stronger password.
9. Verify that there are no password composition rules limiting the type of characters permitted. There should be no requirement for upper or lower case or numbers or special characters.
10. Verify that there are no periodic credential rotation or password history requirements.
11. Verify that "paste" functionality, browser password helpers, and external password managers are permitted.
12. Verify that the user can choose to either temporarily view the entire masked password, or temporarily view the last typed character of the password on platforms that do not have this as native functionality.

### V2.2 General Authenticator Requirements

**Low, medium and high requirements:** 

1. Verify that anti-automation controls are effective at mitigating breached credential testing, brute force, and account lockout attacks. Such controls include blocking the most common breached passwords, soft lockouts, rate limiting, CAPTCHA, ever increasing delays between attempts, IP address restrictions, or risk-based restrictions such as location, first login on a device, recent attempts to unlock the account, or similar. Verify that no more than 100 failed attempts per hour is possible on a single account.
2. Verify that the use of weak authenticators \(such as SMS and email\) is limited to secondary verification and transaction approval and not as a replacement for more secure authentication methods. Verify that stronger methods are offered before weak methods, users are aware of the risks, or that proper measures are in place to limit the risks of account compromise.

### V3.4 Cookie-based Session Management

**Low, medium and high requirements:** 

1. Verify that cookie-based session tokens have the 'Secure' attribute set.
2. Verify that cookie-based session tokens have the 'HttpOnly' attribute set.
3. Verify that cookie-based session tokens utilize the 'SameSite' attribute to limit exposure to cross-site request forgery attacks.
4. Verify that cookie-based session tokens use "\_\_Host-" prefix to provide session cookie confidentiality.
5. Verify that if the application is published under a domain name with other applications that set or use session cookies that might override or disclose the session cookies, set the path attribute in cookie-based session tokens using the most precise path possible.

### V4.2 Operation Level Access Control

**Low, medium and high requirements:** 

1. Verify that sensitive data and APIs are protected against direct object attacks targeting creation, reading, updating and deletion of records, such as creating or updating someone else's record, viewing everyone's records, or deleting all records.
2. Verify that the application or framework enforces a strong anti-CSRF mechanism to protect authenticated functionality, and effective anti-automation or anti-CSRF protects unauthenticated functionality.

### V4.3 Other Access Control Considerations

**Low, medium and high requirements:** 

1. Verify administrative interfaces use appropriate multi-factor authentication to prevent unauthorized use.
2. Verify that directory browsing is disabled unless deliberately desired. Additionally, applications should not allow discovery or disclosure of file or directory metadata, such as Thumbs.db, .DS\_Store, .git or .svn folders.

**Medium and high requirements only:** 

1. Verify the application has additional authorization \(such as step up or adaptive authentication\) for lower value systems, and / or segregation of duties for high value applications to enforce anti-fraud controls as per the risk of application and past fraud.

### V5.1 Input Validation Requirements

**Low, medium and high requirements:** 

1. Verify that the application has defenses against HTTP parameter pollution attacks, particularly if the application framework makes no distinction about the source of request parameters \(GET, POST, cookies, headers, or environment variables\).
2. Verify that frameworks protect against mass parameter assignment attacks, or that the application has countermeasures to protect against unsafe parameter assignment, such as marking fields private or similar.
3. Verify that all input \(HTML form fields, REST requests, URL parameters, HTTP headers, cookies, batch files, RSS feeds, etc\) is validated using positive validation \(whitelisting\).
4. Verify that structured data is strongly typed and validated against a defined schema including allowed characters, length and pattern \(e.g. credit card numbers or telephone, or validating that two related fields are reasonable, such as checking that suburb and zip/postcode match\).
5. Verify that URL redirects and forwards only allow whitelisted destinations, or show a warning when redirecting to potentially untrusted content.

### V8.2 Client-side Data Protection

**Low, medium and high requirements:**

1. Verify the application sets sufficient anti-caching headers so that sensitive data is not cached in modern browsers.
2. Verify that data stored in client side storage \(such as HTML5 local storage, session storage, IndexedDB, regular cookies or Flash cookies\) does not contain sensitive data or PII.
3. Verify that authenticated data is cleared from client storage, such as the browser DOM, after the client or session is terminated.

### V8.3 Sensitive Private Data

**Low, medium and high requirements:**

1. Verify that sensitive data is sent to the server in the HTTP message body or headers, and that query string parameters from any HTTP verb do not contain sensitive data.
2. Verify that users have a method to remove or export their data on demand.
3. Verify that users are provided clear language regarding collection and use of supplied personal information and that users have provided opt-in consent for the use of that data before it is used in any way.

### V12.5 File Download Requirements

**Low, medium and high requirements:**

1. Verify that the web tier is configured to serve only files with specific file extensions to prevent unintentional information and source code leakage. For example, backup files \(e.g. .bak\), temporary working files \(e.g. .swp\), compressed files \(.zip, .tar.gz, etc\) and other extensions commonly used by editors should be blocked unless required.
2. Verify that direct requests to uploaded files will never be executed as HTML/JavaScript content.

