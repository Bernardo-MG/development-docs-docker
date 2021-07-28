# IPs

## Using alias

```text
CMD java -jar centros.war --spring.data.mongodb.host=host.docker.internal
```

## Finding IP to host

```text
CMD export DOCKER_HOST_IP=$(route -n | awk '/UG[ \t]/{print $2}')

CMD java -jar centros.war --spring.data.mongodb.host=$DOCKER_HOST_IP
```

