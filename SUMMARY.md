# Table of contents

* [About](README.md)

## Management hints

* [How to connect security to business](management-hints/connect-security-with-business/README.md)
  * [Bugs severity for a business](management-hints/connect-security-with-business/bugs-severity-for-a-business.md)
  * [Products catalog](management-hints/connect-security-with-business/products-catalog.md)
  * [Risks analysis \(Applications\)](management-hints/connect-security-with-business/risks-analysis.md)
  * [Conclusions](management-hints/connect-security-with-business/conclusions.md)

---

* [SDLC \(Secure Development Lifecycle\)](sdlc-secure-development-lifecycle.md)
* [ASVS V4 Checklists](asvs-v4-checklists.md)
* [Front, back end Checklists](front-back-end-checklists.md)
* [Front, back end Checklists \(rus\)](front-back-end-checklists-rus.md)

## Practices implementation

* [Design](practices-implementation/design/README.md)
  * [Best practices for developers](practices-implementation/design/best-practices-for-developers/README.md)
    * [DevOps](practices-implementation/design/best-practices-for-developers/devops/README.md)
      * [Docker](practices-implementation/design/best-practices-for-developers/devops/docker/README.md)
        * [Running Docker container in rootless mode](practices-implementation/design/best-practices-for-developers/devops/docker/running-docker-container-in-rootless-mode/README.md)
          * [Запуск Docker контейнера без root-прав](practices-implementation/design/best-practices-for-developers/devops/docker/running-docker-container-in-rootless-mode/zapusk-docker-konteinera-bez-root-prav.md)
        * [Running Docker in rootless mode in ubuntu](practices-implementation/design/best-practices-for-developers/devops/docker/running-docker-in-rootless-mode-in-ubuntu/README.md)
          * [Запуск docker в режиме rootless на ubuntu](practices-implementation/design/best-practices-for-developers/devops/docker/running-docker-in-rootless-mode-in-ubuntu/zapusk-docker-v-rezhime-rootless-na-ubuntu.md)
        * [Docker-compose](practices-implementation/design/best-practices-for-developers/devops/docker/docker-compose/README.md)
          * [Volumes, bind mounts or tmpfs mounts](practices-implementation/design/best-practices-for-developers/devops/docker/docker-compose/volumes-bind-mounts-or-tmpfs-mounts/README.md)
            * [Volumes, bind mounts или tmpfs mounts](practices-implementation/design/best-practices-for-developers/devops/docker/docker-compose/volumes-bind-mounts-or-tmpfs-mounts/untitled.md)
          * [Bind mounts](practices-implementation/design/best-practices-for-developers/devops/docker/docker-compose/bind-mounts/README.md)
            * [Bind mounts \(rus\)](practices-implementation/design/best-practices-for-developers/devops/docker/docker-compose/bind-mounts/bind-mounts-rus.md)
          * [tmpfs mounts](practices-implementation/design/best-practices-for-developers/devops/docker/docker-compose/tmpfs-mounts/README.md)
            * [tmpfs mounts \(rus\)](practices-implementation/design/best-practices-for-developers/devops/docker/docker-compose/tmpfs-mounts/tmpfs-mounts-rus.md)
          * [Volumes](practices-implementation/design/best-practices-for-developers/devops/docker/docker-compose/volumes/README.md)
            * [Volumes \(rus\)](practices-implementation/design/best-practices-for-developers/devops/docker/docker-compose/volumes/volumes-rus.md)
      * [Commits signing](practices-implementation/design/best-practices-for-developers/devops/commits-signing.md)
      * [Images signing](practices-implementation/design/best-practices-for-developers/devops/images-signing.md)
    * [Authentication](practices-implementation/design/best-practices-for-developers/identification-authentication-and-authorization-algorithms/README.md)
      * [JSON Web Tokens](practices-implementation/design/best-practices-for-developers/identification-authentication-and-authorization-algorithms/jason-web-token/README.md)
        * [JWT Algorithms use cases](practices-implementation/design/best-practices-for-developers/identification-authentication-and-authorization-algorithms/jason-web-token/jwt-algorithms-use-cases/README.md)
          * [JWT Алгоритмы: варианты использования](practices-implementation/design/best-practices-for-developers/identification-authentication-and-authorization-algorithms/jason-web-token/jwt-algorithms-use-cases/jwt-algoritmy-varianty-ispolzovaniya.md)
      * [Session-based authentication](practices-implementation/design/best-practices-for-developers/identification-authentication-and-authorization-algorithms/session-based-authentication/README.md)
        * [Аутентификация в сессиях](practices-implementation/design/best-practices-for-developers/identification-authentication-and-authorization-algorithms/session-based-authentication/autentifikaciya-v-sessiyakh.md)
      * [OpenID connect \(OIDC\)](practices-implementation/design/best-practices-for-developers/identification-authentication-and-authorization-algorithms/openid-connect-oidc.md)
    * [Authorization](practices-implementation/design/best-practices-for-developers/authorization/README.md)
      * [OAuth 2.0](practices-implementation/design/best-practices-for-developers/authorization/oauth-2.0/README.md)
        * [OAuth 2.0 \(rus\)](practices-implementation/design/best-practices-for-developers/authorization/oauth-2.0/oauth-2.0-rus.md)
    * [Secrets management](practices-implementation/design/best-practices-for-developers/secrets-management.md)
    * [File upload](practices-implementation/design/best-practices-for-developers/file-upload/README.md)
      * [Загрузка файлов](practices-implementation/design/best-practices-for-developers/file-upload/zagruzka-failov.md)
  * [Security requirements](practices-implementation/design/security-requirements.md)
  * [Design review](practices-implementation/design/design-review.md)
* [Implementation](practices-implementation/implementation/README.md)
  * [Code review with static analysers](practices-implementation/implementation/code-review.md)
  * [Implementation review with dynamic analysers](practices-implementation/implementation/implementation-review.md)
* [Asset discovery](practices-implementation/asset-discovery.md)
* [BugBounty](practices-implementation/bugbounty.md)
* [Security champions](practices-implementation/security-champions.md)
* [Continuous Phishing simulations](practices-implementation/continuous-phishing-simulations.md)

## Useful Tools

* [Scanners](useful-tools/scanners/README.md)
  * [Discovery tools](useful-tools/scanners/discovery-tools.md)
  * [Dependency checker](useful-tools/scanners/dependency-checker.md)
  * [SAST](useful-tools/scanners/sast.md)
  * [DAST](useful-tools/scanners/dast.md)
  * [Cloud Security](useful-tools/scanners/cloud-security.md)
* [Services](useful-tools/services/README.md)
  * [Jenkins](useful-tools/services/jenkins.md)
  * [SecureCodeBox](useful-tools/services/securecodebox.md)
  * [SonarQube](useful-tools/services/sonarqube.md)
  * [MobSF](useful-tools/services/mobsf.md)
  * [DefectDojo](useful-tools/services/defectdojo.md)
  * [GoPhish](useful-tools/services/gophish.md)

## Hack space

* [OSINT](hack-space/osint/README.md)
  * [Secrets exploiting](hack-space/osint/secrets.md)
* [Mobile](hack-space/mobile/README.md)
  * [Android](hack-space/mobile/android-checks.md)
* [WEB](hack-space/web/README.md)
  * [Takeovers](hack-space/web/takeovers.md)
  * [Bypasses](hack-space/web/bypasses.md)
  * [Remote Code Execution](hack-space/web/remote-code-execution.md)
  * [SQL injections](hack-space/web/sql-injections.md)

