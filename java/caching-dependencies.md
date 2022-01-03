# Caching Dependencies

```docker
# Resolve and cache dependencies
COPY ./pom.xml .
RUN mvn dependency:resolve
```
