<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
TOC

- [Initialize project](#initialize-project)
  - [Project structure](#project-structure)
  - [Common Library](#common-library)
  - [DevOps](#devops)
    - [NestJS docker image for a service:](#nestjs-docker-image-for-a-service)
    - [Service deployment yaml:](#service-deployment-yaml)
    - [Event Broker with RabbitMQ - deployment yaml](#event-broker-with-rabbitmq---deployment-yaml)
    - [Ingress service](#ingress-service)
  - [Basic dependencies](#basic-dependencies)
  - [Database dependencies (postgres)](#database-dependencies-postgres)
  - [Authentication dependencies](#authentication-dependencies)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Initialize project

## Project structure
- every service is in a separate folder
- every service is generated with ```nest new app```
- place kubernetes yaml files into ```infra/k8s```
- make a folder called "common" for common libraries, so all the services can use it from one place. or just share codes

## Common Library
- sharing code through npm package manager is an efficient way
- [barrel export pattern](https://medium.com/@klauskpm/do-a-barrel-export-aa5b79b76b05)
- initialize a new typescript project with ```init tsc```
- optimize tsconfig for NestJS
```tsconfig
{
  "compilerOptions": {
    /* Visit https://aka.ms/tsconfig to read more about this file */

    /* Projects */
    "incremental": true,                              /* Save .tsbuildinfo files to allow for incremental compilation of projects. */

    /* Language and Environment */
    "target": "ES2017",                                  /* Set the JavaScript language version for emitted JavaScript and include compatible library declarations. */
    "experimentalDecorators": true,                   /* Enable experimental support for TC39 stage 2 draft decorators. */
    "emitDecoratorMetadata": true,                    /* Emit design-type metadata for decorated declarations in source files. */

    /* Modules */
    "module": "commonjs",                                /* Specify what module code is generated. */
    "baseUrl": "./",                                  /* Specify the base directory to resolve non-relative module names. */

    /* Emit */
    "declaration": true,                              /* Generate .d.ts files from TypeScript and JavaScript files in your project. */
    "sourceMap": true,                                /* Create source map files for emitted JavaScript files. */
    "outDir": "./build",                                   /* Specify an output folder for all emitted files. */
    "removeComments": true,                           /* Disable emitting comments. */

    /* Interop Constraints */
    "allowSyntheticDefaultImports": true,             /* Allow 'import x from y' when a module doesn't have a default export. */
    "esModuleInterop": true,                             /* Emit additional JavaScript to ease support for importing CommonJS modules. This enables 'allowSyntheticDefaultImports' for type compatibility. */
    "forceConsistentCasingInFileNames": false,            /* Ensure that casing is correct in imports. */

    /* Type Checking */
    "strict": true,                                      /* Enable all strict type-checking options. */
    "noImplicitAny": false,                            /* Enable error reporting for expressions and declarations with an implied 'any' type. */
    "strictNullChecks": false,                         /* When type checking, take into account 'null' and 'undefined'. */
    "strictBindCallApply": false,                      /* Check that the arguments for 'bind', 'call', and 'apply' methods match the original function. */
    "noFallthroughCasesInSwitch": false,               /* Enable error reporting for fallthrough cases in switch statements. */

    /* Completeness */
    "skipLibCheck": true                                 /* Skip type checking all .d.ts files. */
  }
}

```
- package.json example:
```json
{
  "name": "@cms-microservices/common",
  "version": "1.0.4",
  "description": "",
  "main": "./build/index.js",
  "types": "./build/index.d.ts",
  "files": [
    "build/**/*"
  ],
  "scripts": {
    "clean": "del ./build/*",
    "build": "npm run clean && tsc",
    "pub": "npm version patch && npm run build && npm publish --registry http://165.22.205.66:9000/"
  },
  "author": "Kiss Tamás",
  "license": "ISC",
  "dependencies": {
    "@nestjs/common": "^9.1.4",
    "@nestjs/config": "^2.2.0",
    "@nestjs/microservices": "^9.1.4"
  },
  "devDependencies": {
    "del-cli": "^5.0.0",
    "typescript": "^4.8.4"
  }
}

```
- own npm registry: https://verdaccio.org/

```dockerfile
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

- enable kubernetes in Docker desktop
- API Gateway/BFF (Backend for Frontends) pattern (https://microservices.io/patterns/apigateway.html)
- apply the Nginx Ingress:
```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.4.0/deploy/static/provider/cloud/deploy.yaml
```

### NestJS docker image for a service:
```dockerfile
FROM node:alpine As development

WORKDIR /usr/src/app

COPY package*.json ./
COPY yarn.lock ./

RUN yarn

COPY . .

CMD ["yarn", "start:dev"]
```

### Service deployment yaml:
```yaml
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

### Event Broker with RabbitMQ - deployment yaml
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: rabbitmq-depl
spec:
  replicas: 3
  selector:
    matchLabels:
      app: rabbitmq
  template:
    metadata:
      labels:
        app: rabbitmq
    spec:
      containers:
        - name: rabbitmq
          image: rabbitmq
---
apiVersion: v1
kind: Service
metadata:
  name: rabbitmq-srv
spec:
  selector:
    app: rabbitmq
  ports:
    - name: amqp
      protocol: TCP
      port: 5672
      targetPort: 5672
```

### Ingress service
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-service
  annotations:
    kubernetes.io/ingress.class: nginx
    nginx.ingress.kubernetes.io/use-regex: "true"
spec:
  rules:
    - host: cms-microservices.dev
      http:
        paths:
          - path: /api/?(.*)
            pathType: Prefix
            backend:
              service:
                name: api-gateway-srv
                port:
                  number: 5000
```


## Basic dependencies
- dto validation, class transformation: 
```bash
yarn add class-validator class-transformer
```

## Database dependencies (postgres)
```bash
yarn add @nestjs/typeorm typeorm pg
```

## Authentication dependencies
```bash
yarn add bcrypt
```
```bash
yarn add -D @types/bcrypt
```
```bash
yarn add @nestjs/jwt @nestjs/passport cookie-parser passport passport-jwt passport-local
```
```bash
yarn add -D @types/cookie-parser @types/passport-jwt @types/passport-local
```
