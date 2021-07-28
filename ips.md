# IPs

## Finding IP to host

```text
RUN export DOCKER_HOST_IP=$(route -n | awk '/UG[ \t]/{print $2}')

CMD java -jar centros.war --spring.data.mongodb.host=$DOCKER_HOST_IP
```

