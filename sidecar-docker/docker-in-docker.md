# Docker in Docker

```text
FROM docker:dind
```

```text
docker run -d image --privileged -v /var/run/docker.sock:/var/run/docker.sock
```

