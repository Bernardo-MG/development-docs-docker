# IPs

## Using alias

```
CMD java -jar centros.war --spring.data.mongodb.host=host.docker.internal
```

## Finding IP to host

```
CMD export DOCKER_HOST_IP=$(route -n | awk '/UG[ \t]/{print $2}')

CMD java -jar centros.war --spring.data.mongodb.host=$DOCKER_HOST_IP
```

## Docker Compose Network

Connecting to the host localhost

```
services:
    api:
        environment:
            - spring.data.mongodb.host=127.0.0.1
        network_mode: host
```

