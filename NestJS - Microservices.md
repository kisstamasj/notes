# Initialize project

## Making monorepo
1. `nest new app-name`
2. cd into `app-name` folder
3. `nest generate app service-name`
4. remove the firstly created folder from the `apps` folder
5. also remove that from the `nest-cli.json` file
6. in the `nest-cli.json` correct the `root` property and also the `tsconfigPath` and `sourceRoot`

## Starting the apps
1. yarn dev -> starts the main app
2. yarn dev `service` -> start the selected app/service

Package install only for the main app, and all the other can access them.

## Basic dependencies
- dto validation, class transformation: ```yarn add class-validator class-transformer```

## Database dependencies (postgres)
- ```yarn add @nestjs/typeorm typeorm pg```

## Authentication dependencies
- ```yarn add bcrypt```
- ```yarn add -D @types/bcrypt```
- ```yarn add @nestjs/jwt @nestjs/passport cookie-parser passport passport-jwt passport-local```
