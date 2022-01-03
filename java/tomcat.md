# Tomcat

```docker
# -----------------------------------------------------------------------------
# BUILD STAGE
# -----------------------------------------------------------------------------
FROM maven:3.8.1-jdk-8 as build

# Create app directory
WORKDIR /usr/src/app

# Resolve and cache dependencies
COPY ./pom.xml .
RUN mvn dependency:resolve

# Copy and build
COPY ./ ./
RUN mvn clean package -am -DskipTests

# -----------------------------------------------------------------------------
# DEPLOYMENT STAGE
# -----------------------------------------------------------------------------
FROM tomcat:8 as deployment

# Copy from build stage
COPY --from=build /usr/src/app/target/app.war /usr/local/tomcat/webapps/

EXPOSE 8080
EXPOSE 8000

```

### Remote Debugging

```docker
# Remote debugging
ENV JPDA_TRANSPORT=dt_socket
ENV JPDA_ADDRESS=*:8000

CMD ["catalina.sh","jpda","run"]
```

## Docker Compose

```yaml
version: '3'
services:
   db:
      image: 'db:v1.0.0'
      container_name: sample-db
      ports:yaml
         - '3306:3306'
   api:
      build:
         context: ../
         dockerfile: ./docker/Dockerfile
      container_name: rest-api
      depends_on:
         db:
            condition: service_healthy
      links:
         - db
      ports:
         - '8081:8080'
         - '8000:8000'

```
