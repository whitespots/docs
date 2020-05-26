# Dependency checker

* [dagda](https://github.com/eliasgranderubio/dagda)
* [anchore](https://anchore.com/)

```text
anchore-cli --url http://<anchore_instance>:8228 --u admin -p admin system feeds list
anchore-cli --url http://<anchore_instance>:8228 --u admin -p admin --json image vuln repo/image os > docker_vuln.json
```

* [clair](https://github.com/arminc/clair-scanner)
* [trivy](https://github.com/aquasecurity/trivy)

```text
All instructions here
<https://github.com/aquasecurity/trivy>
```

* [OWASP Dependency checker](https://jeremylong.github.io/DependencyCheck/dependency-check-cli/index.html)

```text
./dependency_check.sh --project 'myapp' --scan '/path/to/app' -f JSON
```

## Have questions?

**Website**: [whitespots.io](https://whitespots.io/?utm=appsecwiki)   
**Email**: [sales@whitespots.io](mailto:sales@whitespots.io)

