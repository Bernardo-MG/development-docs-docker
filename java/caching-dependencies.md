# Caching Dependencies

```text
# Resolve and cache dependencies
COPY ./pom.xml .
RUN mvn dependency:resolve
```

