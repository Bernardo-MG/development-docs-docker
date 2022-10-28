# Tomcat

```docker
# -----------------------------------------------------------------------------
# BUILD STAGE
# -----------------------------------------------------------------------------
FROM maven:3.8.2-jdk-11-slim as build

# Create app directory
WORKDIR /usr/src/app

# Resolve and cache dependencies
COPY ./pom.xml .
RUN mvn dependency:resolve

# Copy and build
COPY . .
RUN mvn clean package -DskipTests

# -----------------------------------------------------------------------------
# DEPLOYMENT STAGE
# -----------------------------------------------------------------------------
FROM tomcat:8 as deployment

ARG WAR_NAME

# Copy from build stage
COPY --from=build /usr/src/app/target/*.war /usr/local/tomcat/webapps/$WAR_NAME

# Exposed ports
EXPOSE 8080
EXPOSE 8000
```
