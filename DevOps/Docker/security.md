# Security

* [Disable SUID programs](http://blog.tutum.co/2015/02/03/hardening-containers-disable-suid-programs/)
* [Docker security tuning](https://opensource.com/business/15/3/docker-security-tuning)
* [Docker and SELinux](https://www.youtube.com/watch?v=zWGFqMuEHdw)
* [Make container reliable](http://blog.jelastic.com/2015/04/14/5-key-features-make-containers-reliable-production-applications/)
* [Container Security: Just the Good Parts](https://securityblog.redhat.com/2015/04/29/container-security-just-the-good-parts/)
* [A field guide to Docker security measures](https://zwischenzugs.wordpress.com/2015/05/21/a-field-guide-to-docker-security-measures/)
* [Someone said that 30% of the images on the Docker Registry contain vulnerabilities](http://jpetazzo.github.io/2015/05/27/docker-images-vulnerabilities/)
* [Video: Securing your application using Docker](https://www.youtube.com/watch?v=KmxOXmPhZbk)
* [Using Docker Safely - Adrian Mouat](https://www.youtube.com/watch?v=04LOuMgNj9U)
* [**TUF - The Update Framework**](http://theupdateframework.com/)

```
docker run -d --name my_db --memory 512m --cpu-shares 512 --user nobody --cap-drop all mysql
```

---

* Treat container services just like regular services. Drop privileges as quickly as possible. Do not run Nginx web server as root.
* Use read-only mount points like `/sys`, `/proc/sys`.
* Use capabilities to drop CAP_XX to minimize attack surface.
* Drop kernel capabilities when starting containers.
* Remove network namespace for database container because maybe you don't need it.
* SELinux protect the host system from container processes
* Container processes only write to container files

The `~/.dockercfg` configuration file holds Docker registry authentication credentials, so protect this file! It should be owned by your user with permissions of `0600`

Breaking out of a container requires root privilege.

```
// Using `adduser` in Dockerfile
// Start a container as non-root user
▶ sudo docker run -u deploy
▶ sudo docker create -user deploy
```

## UID:GID

Root (UID 0) inside a container is a jailed root (UID 0) on the host! Don't run as root inside of a container. Containers running application level code never need root access anyway.

```dockerfile
RUN groupadd -r postgres && useradd -r -g postgres postgres
```

* [Docker User Problems and Patterns](https://medium.com/on-docker/what-s-montague-docker-user-problems-and-patterns-79750c504aa1)

## CIS Benchmark

* [Understanding Docker security and best practices](https://blog.docker.com/2015/05/understanding-docker-security-and-best-practices/)

## Capabilities

If your container did not change the UID/GID of any processes, you could drop these capabilities from your container, making it more secure.

```
▶ docker run -d --cap-drop SETUID --cap-drop SETGID --cap-drop FOWNER fedora /bin/sh
```
