# Spring Boot Deployment

```text
FROM openjdk:8-jre-alpine as deployment

WORKDIR /app

# Copy from build stage
COPY --from=build ./usr/src/app/target/project.war ./project.war

EXPOSE 8080

CMD ["java", "-jar", "project.war"]
```

