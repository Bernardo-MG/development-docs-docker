# Spring Boot Deployment

```docker
FROM openjdk:14-alpine as deployment

ARG WAR_NAME

WORKDIR /app

# Copy from build stage
COPY --from=build ./usr/src/app/target/${WAR_NAME}*.war ./app.war

# Exposed ports
EXPOSE 8080
EXPOSE 8000

# Health check
HEALTHCHECK --interval=30s --retries=5 --timeout=10s CMD curl --fail --silent localhost:8081/actuator/health | grep UP || exit 1

# Run with remote debugging
CMD java -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=0.0.0.0:8000 -jar app.war
```
