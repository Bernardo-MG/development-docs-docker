# Building

```bash
FROM node:14 as build

MAINTAINER Envira Sostenible

# Create app directory
WORKDIR /usr/src/app

# Copy dependencies declaration
COPY package*.json ./

# Continuous Integration installation
RUN npm ci

# Copy, build and deploy project
COPY . .
RUN npm run build
```



