# Initialize project

## Project structure
- every service in a separate folder
- every service generated with ```nest new app```
- kubernets yaml files: ```infra/k8s```
- common folder for common libraries, or just share codes

## Common Library
- efficient way to share code with npm package
- own npm registry: https://verdaccio.org/

```
version: '3.1'

services:
  verdaccio:
    image: verdaccio/verdaccio
    container_name: "npm-registry"
    networks:
      - node-network
    environment:
      - VERDACCIO_PORT=4873
    ports:
      - "9000:4873"
    volumes:
      - "./storage:/storage"
      - "./config:/conf"
      - "./plugins:/plugins"
networks:
  node-network:
    driver: bridge
```

## DevOps
### NestJS docker image for a service:
```
FROM node:alpine As development

WORKDIR /usr/src/app

COPY package*.json ./
COPY yarn.lock ./

RUN yarn

COPY . .

CMD ["yarn", "start:dev"]
```
### Service deployment yaml:
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: api-gateway-depl
spec:
  replicas: 1
  selector:
    matchLabels:
      app: api-gateway
  template:
    metadata:
      labels:
        app: api-gateway
    spec:
      containers:
        - name: api-gateway
          image: kisstamas/cms-api-gateway
---
apiVersion: v1
kind: Service
metadata:
  name: api-gateway-srv
spec:
  selector:
    app: api-gateway
  ports:
    - name: api-gateway
      protocol: TCP
      port: 5000
      targetPort: 5000
```

## Basic dependencies
- dto validation, class transformation: ```yarn add class-validator class-transformer```

## Database dependencies (postgres)
- ```yarn add @nestjs/typeorm typeorm pg```

## Authentication dependencies
- ```yarn add bcrypt```
- ```yarn add -D @types/bcrypt```
- ```yarn add @nestjs/jwt @nestjs/passport cookie-parser passport passport-jwt passport-local```
- ```yarn add -D @types/cookie-parser @types/passport-jwt @types/passport-local```
