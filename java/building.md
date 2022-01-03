# Building

```docker
FROM maven:3.8.1-jdk-8 as build

# Create app directory
WORKDIR /usr/src/app

# Copy and build
COPY . .

RUN mvn clean package -DskipTests
```
