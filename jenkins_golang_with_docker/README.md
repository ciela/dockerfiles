Usage
=====

```bash
$ docker run --name dind --privileged -d -p 4444 -e PORT=4444 dind
$ docker run -d -p 8080:8080 --link dind:dind ciela/golang-awseb-jenkins
```

Access
======

```
http://localhost:8080/
```
