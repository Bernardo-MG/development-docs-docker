# Building

```docker
FROM node:14 as build

# Create app directory
WORKDIR /usr/src/app

# Copy dependencies declaration
COPY package*.json ./

# Continuous Integration installation
RUN npm ci

# Copy and build
COPY . .
RUN npm run build
```

