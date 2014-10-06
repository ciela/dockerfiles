Usage
=====

Jenkins内でDocker叩くので一工夫必要。

```bash
$ docker run -d -p 8080:8080 -v /var/run/docker.sock:/var/run/docker.sock ciela/golang-awseb-jenkins
```

とかDocker in Docker使って

```bash
$ docker run --name dind --privileged -d -p 4444 -e PORT=4444 dind
$ docker run -d -p 8080:8080 --link dind:dind ciela/golang-awseb-jenkins
```

とか。

Access
======

```
http://localhost:8080/
```
